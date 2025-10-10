# ColdBox Flat Template - AI Coding Instructions

This is a ColdBox HMVC framework template using the traditional "flat" structure where all application code lives in the webroot. Compatible with Adobe ColdFusion 2018+, Lucee 5.x+, and BoxLang 1.0+.

## 🏗️ Architecture Overview

**Key Design Decision**: Unlike the Modern template which separates `/app` from `/public`, this template uses a flat structure with all files in the webroot. This is simpler for learning, prototyping, and traditional hosting environments.

### Directory Structure

```
/                      - Application root (webroot)
├── Application.cfc    - Bootstrap that directly loads ColdBox
├── index.cfm          - Front controller
├── config/            - Framework and app configuration
│   ├── ColdBox.cfc   - Main framework settings
│   └── Router.cfc    - URL routing definitions
├── handlers/          - Event handlers (controllers)
├── models/            - Service objects, business logic
├── views/             - HTML templates
├── layouts/           - Page layouts wrapping views
├── includes/          - Public assets (CSS, JS, images)
│   └── helpers/      - Application helpers
├── modules_app/       - Application modules (HMVC)
├── tests/             - Test suites
│   └── specs/        - BDD test specifications
└── lib/               - Framework dependencies
    ├── coldbox/      - ColdBox framework (installed via box.json)
    └── testbox/      - TestBox testing framework
```

### Application Bootstrap Flow

1. Request hits `index.cfm` (front controller)
2. `Application.cfc.onApplicationStart()` creates ColdBox Bootstrap and calls `loadColdbox()`
3. Bootstrap sets critical mappings:
   - `COLDBOX_APP_ROOT_PATH = getDirectoryFromPath(getCurrentTemplatePath())` - Root path
   - `COLDBOX_APP_MAPPING = ""` - Empty because app is at root
   - `this.mappings["/app"] = COLDBOX_APP_ROOT_PATH` - Alias for root
   - `this.mappings["/coldbox"] = COLDBOX_APP_ROOT_PATH & "coldbox"` - Framework location
4. ColdBox loads `config/ColdBox.cfc` for framework settings
5. ColdBox loads `config/Router.cfc` for URL routing
6. Request is processed by handler action

## 📝 Handler Patterns

All handlers extend `coldbox.system.EventHandler` and receive three arguments in every action:

```cfml
component extends="coldbox.system.EventHandler" {

    // Dependency injection via properties
    property name="userService" inject="UserService";

    /**
     * Every handler action receives:
     * @event RequestContext object - get/set values, rendering, redirects
     * @rc    Request Collection - URL/FORM variables (untrusted input)
     * @prc   Private Request Collection - handler-to-view data (trusted)
     */
    function index(event, rc, prc){
        // Pass data to view via prc
        prc.welcomeMessage = "Welcome to ColdBox!";
        event.setView("main/index");
    }

    // RESTful data - return any data type, ColdBox handles marshalling
    function data(event, rc, prc){
        return [
            {id: createUUID(), name: "Luis"}
        ];
    }

    // Relocations (internal redirects)
    function doSomething(event, rc, prc){
        relocate("main.index");
    }

    // Optional lifecycle handlers (must be enabled in config/ColdBox.cfc)
    function onAppInit(event, rc, prc){}
    function onRequestStart(event, rc, prc){}
    function onException(event, rc, prc){
        event.setHTTPHeader(statusCode=500);
        var exception = prc.exception; // Populated by ColdBox
    }
}
```

### Critical Pattern: rc vs prc

- **rc (Request Collection)**: Automatically populated with FORM/URL variables. **Never trust this data** - always validate.
- **prc (Private Request Collection)**: Pass data from handlers to views/layouts. **Not accessible from URL**.

## 🧪 Testing Patterns

**CRITICAL**: Tests extend `BaseTestCase` with `appMapping="/app"` pointing to the root mapping defined in Application.cfc:

```cfml
component extends="coldbox.system.testing.BaseTestCase" appMapping="/app" {

    function run(){
        describe("Main Handler", function(){
            beforeEach(function(currentSpec){
                // MUST call setup() to reset request context per test
                setup();
            });

            it("can render the homepage", function(){
                var event = this.get("main.index");
                expect(event.getValue(name="welcomeMessage", private=true))
                    .toBe("Welcome to ColdBox!");
            });

            it("can return RESTful data", function(){
                var event = this.post("main.data");
                expect(event.getRenderedContent()).toBeJSON();
            });
        });
    }
}
```

### Testing Methods

- `this.get(event)` - Execute GET request
- `this.post(event, params)` - Execute POST request
- `execute(event, private, prePostExempt)` - Execute any event
- `getRequestContext()` - Get current request context

### Common Testing Mistakes

❌ **Forgetting `setup()` in `beforeEach()`** - Tests share request context and fail mysteriously
✅ **Always call `setup()`** - Ensures each test gets fresh request context

## 🛠️ Build Commands

```bash
# Install dependencies (coldbox, testbox, dev tools)
box install

# Start server
box server start

# Code formatting
box run-script format              # Format all CFML code
box run-script format:check        # Check formatting without changes
box run-script format:watch        # Watch and auto-format

# Testing
box testbox run                    # Run all tests
box testbox run bundles=tests.specs.integration.MainSpec

# Scaffolding (coldbox-cli)
coldbox create handler name=Users actions=index,create,save
coldbox create model name=UserService methods=getAll,save
coldbox create integration-test handler=Users

# Docker
box run-script docker:build        # Build image
box run-script docker:run          # Run container
box run-script docker:stack up     # Start compose stack
```

## 🎯 Configuration Patterns

### Environment Variables (.env)

The `postInstall` script copies `.env.example` to `.env` automatically. Access values with `getSystemSetting()`:

```cfml
// config/ColdBox.cfc
variables.coldbox = {
    appName: getSystemSetting("APPNAME", "Default App Name")
};

// In handlers/models
var dbHost = getSystemSetting("DB_HOST", "localhost");
```

### Implicit Event Handlers

To enable lifecycle methods, configure in `config/ColdBox.cfc`:

```cfml
variables.coldbox = {
    applicationStartHandler: "Main.onAppInit",
    requestStartHandler: "Main.onRequestStart",
    exceptionHandler: "main.onException"
};
```

### Application Helper

The `includes/helpers/ApplicationHelper.cfm` is automatically available in all handlers, views, and layouts:

```cfml
<!--- includes/helpers/ApplicationHelper.cfm --->
<cfscript>
function formatCurrency(required numeric amount){
    return dollarFormat(arguments.amount);
}
</cfscript>
```

## 🔄 Routing (config/Router.cfc)

```cfml
component {
    function configure(){
        // Closure routes
        route("/healthcheck", function(event, rc, prc){
            return "Ok!";
        });

        // RESTful resources (generates 7 CRUD routes)
        resources("photos");

        // Pattern-based routes
        route("/users/:id").to("users.show");

        // Route groups
        group({prefix: "/api/v1"}, function(){
            route("/users").to("api.users.index");
        });

        // Conventions-based catch-all (MUST be last)
        route(":handler/:action?").end();
    }
}
```

## 💉 Dependency Injection (WireBox)

### Property Injection DSL

```cfml
component {
    // Inject by model name (auto-resolved from models/ folder)
    property name="userService" inject="UserService";

    // Inject by ID
    property name="cache" inject="cachebox:default";

    // Inject logger for this component
    property name="log" inject="logbox:logger:{this}";

    // Provider injection (lazy loading)
    property name="userServiceProvider" inject="provider:UserService";
}
```

### Auto-Discovery of Models

When `autoMapModels=true` in `config/ColdBox.cfc` (default), all CFCs in `models/` are automatically registered:

```
models/
├── UserService.cfc          → inject="UserService"
├── security/
│   └── AuthService.cfc      → inject="security.AuthService"
```

## ☕ Java Dependencies (Maven)

The template includes `pom.xml` for Java library management:

```bash
# Add dependencies to pom.xml, then:
mvn install    # Download JARs to lib/ folder
mvn clean      # Remove all JARs
```

`Application.cfc` automatically loads JARs via `this.javaSettings.loadPaths = [expandPath("./lib")]`.

## 🚨 Common Pitfalls

1. **Test Isolation**: Forgetting `setup()` in `beforeEach()` causes shared request context
2. **appMapping**: Tests require `appMapping="/app"` to match `Application.cfc` mapping
3. **Environment Variables**: `.env` is auto-created from `.env.example` by postInstall
4. **Framework Reinit**: Use `?fwreinit=true` or configure `reinitPassword` for production
5. **Library Paths**: `box.json` installs to `coldbox/` and `testbox/` (not `lib/coldbox/`)
6. **Implicit Events**: Lifecycle methods like `onAppInit` only fire if configured in `config/ColdBox.cfc`

## 📚 Key Files Reference

- `Application.cfc` - Bootstrap, mappings, lifecycle (onApplicationStart, onRequestStart, etc.)
- `config/ColdBox.cfc` - Framework configuration, environment detection
- `config/Router.cfc` - URL routing definitions
- `box.json` - Dependencies (`coldbox:be`, `testbox`), scripts, settings
- `server.json` - Server engine (boxlang@1), JVM settings, rewrites
- `includes/helpers/ApplicationHelper.cfm` - Global helper functions
- `tests/Application.cfc` - Test bootstrap (mirrors main Application.cfc)

## 🔍 Debugging

```cfml
// Enable debug mode in config/ColdBox.cfc
variables.settings = { debugMode: true };

// Dump in handlers
writeDump(var=rc, abort=true);

// Use injected logger
property name="log" inject="logbox:logger:{this}";
log.info("Debug message", rc);

// TestBox debug helper
debug(event.getHandlerResults());
```

## 📖 Documentation

- ColdBox: https://coldbox.ortusbooks.com
- WireBox: https://wirebox.ortusbooks.com
- TestBox: https://testbox.ortusbooks.com
- CommandBox: https://commandbox.ortusbooks.com
