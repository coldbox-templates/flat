<p align="center">
	<img src="https://www.ortussolutions.com/__media/coldbox-185-logo.png">
	<br>
	<img src="https://www.ortussolutions.com/__media/wirebox-185.png" height="125">
	<img src="https://www.ortussolutions.com/__media/cachebox-185.png" height="125" >
	<img src="https://www.ortussolutions.com/__media/logbox-185.png"  height="125">
</p>

<p align="center">
	<a href="https://github.com/ColdBox/coldbox-platform/actions/workflows/snapshot.yml"><img src="https://github.com/ColdBox/coldbox-platform/actions/workflows/snapshot.yml/badge.svg" alt="ColdBox Snapshots" /></a>
	<a href="https://forgebox.io/view/coldbox"><img src="https://forgebox.io/api/v1/entry/coldbox/badges/downloads" alt="Total Downloads" /></a>
	<a href="https://forgebox.io/view/coldbox"><img src="https://forgebox.io/api/v1/entry/coldbox/badges/version" alt="Latest Stable Version" /></a>
	<a href="https://img.shields.io/badge/License-Apache2-brightgreen"><img src="https://img.shields.io/badge/License-Apache2-brightgreen" alt="Apache2 License" /></a>
</p>

<p align="center">
	Copyright Since 2005 ColdBox Platform by Luis Majano and Ortus Solutions, Corp
	<br>
	<a href="https://www.coldbox.org">www.coldbox.org</a> |
	<a href="https://www.ortussolutions.com">www.ortussolutions.com</a>
</p>

----

# 📦 ColdBox Flat Application Template

Welcome to the **Flat** ColdBox application template! 🎉 This is the traditional, straightforward template for building HMVC (Hierarchical Model-View-Controller) web applications using **Adobe ColdFusion**, **Lucee**, or **BoxLang**.

## 🌟 What is the "Flat" Template?

The Flat template uses the traditional ColdBox structure where all application files reside in the **web root**. This is the most common and widely-used ColdBox template, perfect for:

- **🚀 Quick Prototyping** - Get started fast without complex directory structures
- **📚 Learning ColdBox** - Straightforward layout makes it easy to understand the framework
- **🔧 Simple Deployments** - Traditional hosting setup with minimal configuration
- **🌐 Universal Compatibility** - Works with Adobe CF, Lucee, and BoxLang

> **💡 Perfect for**: Learning projects, rapid prototyping, internal tools, traditional hosting environments, and teams familiar with standard CFML application structures.

> **🔒 Need enhanced security?** Check out the [Modern Template](../modern/) which separates application code from the web root.

## ⚙️ Requirements

Before getting started, ensure you have the following installed on your operating system:

1. **CommandBox** - CLI toolchain, package manager, and server runtime
   - 📥 Installation: <https://commandbox.ortusbooks.com/setup/installation>
   - 📌 Minimum Version: 6.0+
   - 🎯 Used for: dependency management, server starting, testing, and task automation

2. **CFML Engine** - Choose your preferred engine:
   - **Adobe ColdFusion** 2018+ - <https://www.adobe.com/products/coldfusion-family.html>
   - **Lucee** 5.x+ - <https://www.lucee.org>
   - **BoxLang** 1.0+ - <https://boxlang.io>

3. **Java** (Optional) - For Maven-based Java dependencies
   - Required only if using Java libraries via Maven
   - Compatible with Java 11+ (Java 21 recommended)

## 📋 Table of Contents

- [Directory Structure](#-directory-structure)
- [Quick Start](#-quick-start)
- [Application Bootstrap](#-application-bootstrap)
- [Development Workflows](#️-development-workflows)
- [Testing](#-testing)
- [Java Dependencies](#-java-dependencies)
- [Docker Support](#-docker-support)
- [Environment Configuration](#-environment-configuration)
- [Dependency Injection](#-dependency-injection)
- [Handler Patterns](#-handler-patterns)
- [Routing](#-routing)
- [VSCode Helpers](#-vscode-helpers)
- [ColdBox Features](#-coldbox-features)
- [Learning Resources](#-learning-resources)
- [Sponsors](#-sponsors)
- [Important Links](#-important-links)

## 📁 Directory Structure

The Flat template follows the traditional ColdBox HMVC structure with all files in the web root:

```
├── 📄 Application.cfc          # Application bootstrap & settings
├── 📄 index.cfm                # Front controller
├── 🎨 favicon.ico              # Site favicon
├── 🤖 robots.txt               # SEO robots file
│
├── 📂 config/                  # Application configuration
│   ├── ColdBox.cfc            # Framework settings
│   ├── Router.cfc             # URL routing definitions
│   └── WireBox.cfc            # Optional DI mappings
│
├── 📂 handlers/                # Event handlers (controllers)
│   └── Main.cfc               # Default handler
│
├── 📂 models/                  # Business logic layer
│   └── (your models here)
│
├── 📂 views/                   # View templates
│   └── main/                  # Views for Main handler
│
├── 📂 layouts/                 # Layout templates
│   └── Main.cfm               # Default layout
│
├── 📂 includes/                # Public assets (CSS, JS, images)
│   ├── css/
│   ├── js/
│   └── images/
│
├── 📂 modules_app/             # Application modules
│   └── (your modules here)
│
├── 📂 tests/                   # Test suites
│   ├── specs/                 # Test specifications
│   │   ├── integration/       # Integration tests
│   │   └── unit/              # Unit tests
│   ├── Application.cfc        # Test bootstrap
│   └── runner.cfm             # Test runner
│
├── 📂 lib/                     # Framework libraries
│   ├── coldbox/               # ColdBox framework
│   └── testbox/               # TestBox testing framework
│
├── 📂 docker/                  # Docker configuration
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── 📄 box.json                 # CommandBox package descriptor
├── 📄 server.json              # Server configuration
├── 📄 .env                     # Environment variables
├── 📄 pom.xml                  # Maven Java dependencies
└── 📄 .cfformat.json           # Code formatting rules
```

### Key Directories

- **`handlers/`** - Event handlers (controllers) that respond to user requests
- **`models/`** - Service objects, beans, and business logic
- **`views/`** - HTML templates rendered by handlers
- **`layouts/`** - Page layouts that wrap views
- **`config/`** - Application and framework configuration
- **`tests/`** - BDD/TDD test suites using TestBox
- **`modules_app/`** - Modular HMVC applications within your app
- **`lib/`** - Third-party frameworks installed by CommandBox

## 🚀 Quick Start

### 1. Install Dependencies

First, install all required dependencies including ColdBox and TestBox:

```bash
box install
```

This command reads `box.json` and installs:
- **ColdBox** framework to `lib/coldbox/`
- **TestBox** testing framework to `lib/testbox/`
- **Development tools** (cfformat, coldbox-cli, testbox-cli)

### 2. Start the Server

Start the embedded CommandBox server:

```bash
box server start
```

The application will be available at: **<http://localhost:PORT>** (CommandBox will display the actual port)

### 3. View Your Application

Open your browser and navigate to the server URL. You should see the ColdBox welcome page!

### 4. Start Coding

- **Create handlers**: `coldbox create handler name=YourHandler actions=index,save`
- **Create models**: `coldbox create model name=UserService`
- **Create tests**: `coldbox create integration-test handler=YourHandler`

## 🔧 Application Bootstrap

### How It Works

The Flat template uses a simple bootstrap flow:

```
┌─────────────────────────────────────────────────────────────┐
│ 1. User Request → index.cfm (Front Controller)              │
│ 2. index.cfm calls Application.cfc                          │
│ 3. Application.cfc bootstraps ColdBox framework             │
│ 4. ColdBox loads config/ColdBox.cfc                         │
│ 5. ColdBox loads config/Router.cfc                          │
│ 6. ColdBox executes handler action                          │
│ 7. Handler renders view/layout or returns data              │
└─────────────────────────────────────────────────────────────┘
```

### Key Configuration Files

**`Application.cfc`** - Application bootstrap:
```cfml
component {
    this.name = "My ColdBox Application";
    this.sessionManagement = true;

    // ColdBox Bootstrap Settings
    COLDBOX_APP_ROOT_PATH = getDirectoryFromPath(getCurrentTemplatePath());
    COLDBOX_APP_MAPPING = "";
    COLDBOX_CONFIG_FILE = "";

    // Java integration for lib/ folder
    this.javaSettings = {
        loadPaths: [expandPath("./lib")]
    };
}
```

**`config/ColdBox.cfc`** - Framework configuration:
- Application name and settings
- Event handlers and implicit events
- Module locations
- Caching strategies
- Logging configuration

**`config/Router.cfc`** - URL routing:
- RESTful API routes
- Resource routes
- Conventions-based routing

## 🛠️ Development Workflows

### Code Formatting

Format your code using CFFormat:

```bash
# Format all CFML code
box run-script format

# Check formatting without changes
box run-script format:check

# Watch for changes and auto-format
box run-script format:watch
```

### Running Tests

Execute your test suites:

```bash
# Run all tests
box testbox run

# Run specific test bundle
box testbox run bundles=tests.specs.integration.MainSpec

# Run with coverage
box testbox run --verbose
```

### Creating Scaffolding

Use ColdBox CLI to generate code:

```bash
# Create a handler with actions
coldbox create handler name=Users actions=index,create,save,delete

# Create a model with unit test
coldbox create model name=UserService methods=getAll,save,delete --open

# Create an integration test
coldbox create integration-test handler=Users

# Create a complete REST resource (handler + views + tests)
coldbox create resource name=Products --plural
```

### Server Management

```bash
# Start server
box server start

# Stop server
box server stop

# Restart server
box server restart

# Open server in browser
box server open

# View server logs
box server log
```

## 🧪 Testing

The Flat template includes a comprehensive testing setup using **TestBox**, a BDD/TDD testing framework.

### Test Structure

```
tests/
├── Application.cfc          # Test bootstrap
├── runner.cfm               # Browser test runner
└── specs/
    ├── integration/         # Integration tests (test full request lifecycle)
    │   └── MainSpec.cfc
    └── unit/                # Unit tests (test individual components)
        └── (your tests here)
```

### Running Tests

```bash
# Run all tests
box testbox run

# Run specific test bundle
box testbox run bundles=tests.specs.integration.MainSpec

# Run tests and generate coverage report
box testbox run --verbose

# Run tests in browser
box server start
# Navigate to: http://localhost:PORT/tests/runner.cfm
```

### Writing Integration Tests

Integration tests extend `coldbox.system.testing.BaseTestCase`:

```cfml
component extends="coldbox.system.testing.BaseTestCase" {

    function beforeAll() {
        super.beforeAll();
    }

    function run() {
        describe("Main Handler", function() {
            beforeEach(function(currentSpec) {
                // CRITICAL: Call setup() to reset request context
                setup();
            });

            it("can render the homepage", function() {
                var event = this.get("main.index");
                expect(event.getValue(name="welcomeMessage", private=true))
                    .toBe("Welcome to ColdBox!");
            });

            it("can return RESTful data", function() {
                var event = this.post("main.data");
                expect(event.getRenderedContent()).toBeJSON();
            });

            it("can handle relocations", function() {
                var event = execute(event="main.doSomething");
                expect(event.getValue("relocate_event", "")).toBe("main.index");
            });
        });
    }
}
```

### Testing Helpers

The `BaseTestCase` provides helpful methods:

- **`this.get(event)`** - Execute GET request
- **`this.post(event, params)`** - Execute POST request
- **`this.put(event, params)`** - Execute PUT request
- **`this.delete(event)`** - Execute DELETE request
- **`execute(event, private, prePostExempt)`** - Execute any event
- **`getRequestContext()`** - Get current request context

### Best Practices

✅ **Always call `setup()`** in `beforeEach()` to reset the request context
✅ **Test one thing** per test case
✅ **Use descriptive names** for your test suites and specs
✅ **Test both success and failure** paths
✅ **Mock external dependencies** to isolate your tests

## ☕ Java Dependencies

If your project relies on Java third-party libraries, you can use the included Maven `pom.xml` file.

### Adding Java Dependencies

1. **Find your dependency** at <https://central.sonatype.com/>
2. **Copy the Maven coordinates** (groupId, artifactId, version)
3. **Add to `pom.xml`**:

```xml
<dependencies>
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.10.1</version>
    </dependency>
</dependencies>
```

4. **Download the JARs**:

```bash
mvn install
```

This downloads all JARs to the `lib/` folder, which is automatically loaded by `Application.cfc` via `this.javaSettings.loadPaths`.

### Managing Java Dependencies

```bash
# Install/update dependencies
mvn install

# Remove all downloaded JARs
mvn clean

# Update all dependencies to latest versions
mvn versions:use-latest-versions
```

### Automatic Class Loading

The `Application.cfc` automatically loads all JARs from the `lib/` folder:

```cfml
this.javaSettings = {
    loadPaths: [expandPath("./lib")],
    loadColdFusionClassPath: true,
    reloadOnChange: false
};
```

## 🐳 Docker Support

The template includes Docker configuration for containerized deployments.

### Building Docker Images

Build a Docker image using the CommandBox base image:

```bash
# Build the image
box run-script docker:build

# Run the container
box run-script docker:run

# Access container bash
box run-script docker:bash
```

### Docker Compose Stack

The template includes a `docker-compose.yml` file with support for multiple databases:

```bash
# Start the stack (app + database)
box run-script docker:stack up

# Stop the stack
box run-script docker:stack down

# View logs
box run-script docker:stack logs
```

**Supported Databases:**
- MySQL
- PostgreSQL
- Microsoft SQL Server

Edit `docker/docker-compose.yml` to configure your preferred database.

### Dockerfile

The included `docker/Dockerfile` uses the official CommandBox Docker image:

```dockerfile
FROM ortussolutions/commandbox:latest

# Copy app files
COPY . /app

# Install dependencies
RUN box install

# Expose port
EXPOSE 8080

# Start server
CMD ["box", "server", "start"]
```

## 🌍 Environment Configuration

The template uses a `.env` file for environment-specific configuration.

### Setup

1. **Copy the example file**:

```bash
cp .env.example .env
```

2. **Edit `.env`** with your settings:

```properties
# Application Settings
APPNAME=My Awesome App
ENVIRONMENT=development

# Database Settings
DB_HOST=localhost
DB_PORT=3306
DB_NAME=myapp
DB_USER=root
DB_PASSWORD=secret

# API Keys
API_KEY=your-api-key-here
```

3. **Access in your code** using `getSystemSetting()`:

```cfml
// In config/ColdBox.cfc
variables.coldbox = {
    appName: getSystemSetting("APPNAME", "Default App Name")
};

// In your handlers/models
var dbHost = getSystemSetting("DB_HOST", "localhost");
var apiKey = getSystemSetting("API_KEY");
```

### Environment Detection

The template automatically detects the environment:

- **Development** - Local development machine
- **Staging** - Pre-production environment
- **Production** - Live environment

Configure environment-specific settings in `config/ColdBox.cfc`:

```cfml
function development() {
    variables.coldbox.handlersIndexAutoReload = true;
}

function production() {
    variables.coldbox.handlersIndexAutoReload = false;
    variables.coldbox.handlerCaching = true;
}
```

## 💉 Dependency Injection

The Flat template leverages **WireBox**, ColdBox's dependency injection framework.

### Basic Injection

Use the `@inject` annotation to inject dependencies:

```cfml
// In a handler
component extends="coldbox.system.EventHandler" {

    property name="userService" inject="UserService";

    function index(event, rc, prc) {
        prc.users = userService.getAll();
        event.setView("users/index");
    }
}
```

### Model Example

```cfml
// models/UserService.cfc
component singleton {

    property name="log" inject="logbox:logger:{this}";

    function getAll() {
        log.info("Fetching all users");
        return queryExecute("SELECT * FROM users");
    }

    function save(required struct data) {
        // Save user logic
    }
}
```

### Injection DSL

WireBox provides a powerful injection DSL:

- **`@inject="model"`** - Inject by model name
- **`@inject="id:MyService"`** - Inject by specific ID
- **`@inject="provider:UserService"`** - Inject a provider (lazy loading)
- **`@inject="logbox:logger:{this}`** - Inject a logger for this component
- **`@inject="cachebox:default"`** - Inject the default cache
- **`@inject="wirebox"`** - Inject the WireBox injector itself

### Configuration

Configure WireBox in `config/WireBox.cfc` (optional):

```cfml
component extends="coldbox.system.ioc.config.Binder" {

    function configure() {
        // Map custom objects
        map("SecurityService").to("models.security.SecurityService");

        // Map interfaces to implementations
        map("IUserService").to("models.UserService");
    }
}
```

## 🎯 Handler Patterns

Handlers (controllers) respond to user requests and coordinate application flow.

### Basic Handler

```cfml
component extends="coldbox.system.EventHandler" {

    /**
     * Default action
     */
    function index(event, rc, prc) {
        prc.welcomeMessage = "Hello World!";
        event.setView("main/index");
    }

    /**
     * RESTful JSON response
     */
    function data(event, rc, prc) {
        return [
            {id: 1, name: "Alice"},
            {id: 2, name: "Bob"}
        ];
    }

    /**
     * Relocation example
     */
    function save(event, rc, prc) {
        // Save logic here
        relocate("main.index");
    }
}
```

### Handler Arguments

Every handler action receives three arguments:

- **`event`** - Request context with methods to get/set values, render views, etc.
- **`rc`** - Request collection (URL and FORM scopes combined)
- **`prc`** - Private request collection (not accessible from URL)

### Common Event Methods

```cfml
// Get request values
var id = event.getValue("id", 0);
var name = event.getPrivateValue("name");

// Set values
event.setValue("result", data);
event.setPrivateValue("user", userObj);

// Rendering
event.setView("users/edit");
event.setLayout("admin");
return event.renderData(data=result, type="json");

// Relocations
event.overrideEvent("users.list");
relocate("users.index");
```

### Lifecycle Methods

Handlers support implicit lifecycle events:

```cfml
function onAppInit(event, rc, prc) {
    // Called once when application starts
}

function onRequestStart(event, rc, prc) {
    // Called before each request
}

function onRequestEnd(event, rc, prc) {
    // Called after each request
}

function onException(event, rc, prc) {
    // Called when an exception occurs
    var exception = prc.exception;
    log.error("Error occurred", exception);
}
```

## 🛣️ Routing

The template uses `config/Router.cfc` to define URL routes.

### Basic Routes

```cfml
component {
    function configure() {
        // Simple route
        route("/about").to("main.about");

        // Route with parameters
        route("/users/:id").to("users.show");

        // Route with closure
        route("/api/health", function(event, rc, prc) {
            return {status: "OK", timestamp: now()};
        });

        // Conventions-based routing (catch-all)
        route(":handler/:action?").end();
    }
}
```

### RESTful Resources

```cfml
resources("photos"); // Creates 7 RESTful routes

// Equivalent to:
// GET    /photos          -> photos.index
// GET    /photos/new      -> photos.new
// POST   /photos          -> photos.create
// GET    /photos/:id      -> photos.show
// GET    /photos/:id/edit -> photos.edit
// PUT    /photos/:id      -> photos.update
// DELETE /photos/:id      -> photos.delete
```

### Route Groups

```cfml
group({prefix: "/api/v1"}, function() {
    route("/users").to("api.users.index");
    route("/products").to("api.products.index");
});
```

## 🔧 VSCode Helpers

The template includes VSCode configuration for enhanced development experience.

### Included Files

- **`.vscode/settings.json`** - IntelliSense for ColdBox and TestBox
- **`.vscode/tasks.json`** - Quick tasks for common operations

### Custom Tasks

**Run CommandBox Task** - Execute CommandBox tasks quickly
**Run TestBox Bundle** - Run tests from current file

**Usage:**
1. Open Command Palette (`Cmd+Shift+P` or `Ctrl+Shift+P`)
2. Select `Tasks: Run Build Task`
3. Or use shortcut: `⇧⌘B` (Mac) / `Shift+Ctrl+B` (Windows)

### Recommended Extensions

Install these VSCode extensions for the best development experience:

- **CFML** by KamasamaK - Language support and IntelliSense
- **CFLint** - CFML linting
- **vscode-coldbox** - ColdBox snippets and commands

## 🎁 ColdBox Features

ColdBox is a professional, conventions-based HMVC framework packed with features:

- [Conventions instead of configuration](https://coldbox.ortusbooks.com/getting-started/conventions)
- [Modern URL routing](https://coldbox.ortusbooks.com/the-basics/routing)
- [RESTFul APIs](https://coldbox.ortusbooks.com/the-basics/event-handlers/rendering-data)
- [Hierarchical MVC with modules](https://coldbox.ortusbooks.com/hmvc/modules)
- [Event-driven programming](https://coldbox.ortusbooks.com/digging-deeper/interceptors)
- [Async and parallel programming](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)
- [Integration & unit testing](https://coldbox.ortusbooks.com/testing/testing-coldbox-applications)
- [Dependency injection with WireBox](https://wirebox.ortusbooks.com)
- [Caching with CacheBox](https://cachebox.ortusbooks.com)
- [Logging with LogBox](https://logbox.ortusbooks.com)
- [Extensive ecosystem](https://forgebox.io)

## 📚 Learning Resources

### Official Documentation

- **ColdBox Docs** - <https://coldbox.ortusbooks.com>
- **WireBox Docs** - <https://wirebox.ortusbooks.com>
- **CacheBox Docs** - <https://cachebox.ortusbooks.com>
- **LogBox Docs** - <https://logbox.ortusbooks.com>
- **TestBox Docs** - <https://testbox.ortusbooks.com>

### Video Learning

**CFCasts** - Premium video training platform
<https://www.cfcasts.com>

Get access to hundreds of ColdBox tutorials, from beginner to advanced topics.

### Community

- **ColdBox Forum** - <https://community.ortussolutions.com>
- **Ortus Slack** - <https://boxteam.ortussolutions.com>
- **Stack Overflow** - Tag your questions with `coldbox`

## 💰 Sponsors

ColdBox is a professional open-source project completely funded by the [community](https://patreon.com/ortussolutions) and [Ortus Solutions, Corp](https://www.ortussolutions.com).

### Become a Sponsor

Support ColdBox development and get awesome benefits:

- 🎥 **CFCasts Account** - Access to premium video training
- 📦 **ForgeBox Pro** - Advanced package management features
- 🎫 **Event Discounts** - Discounts on Into the Box conference
- 🏆 **Recognition** - Your logo on our website and documentation

Visit our Patreon page: <https://patreon.com/ortussolutions>

## 🔗 Important Links

- **Website** - <https://www.coldbox.org>
- **Documentation** - <https://coldbox.ortusbooks.com>
- **GitHub** - <https://github.com/ColdBox/coldbox-platform>
- **ForgeBox** - <https://forgebox.io/view/coldbox>
- **Ortus Solutions** - <https://www.ortussolutions.com>
- **Ortus Community** - <https://community.ortussolutions.com>
- **CFCasts Training** - <https://www.cfcasts.com>

## 📄 License

Apache License, Version 2.0.

See [LICENSE](https://www.apache.org/licenses/LICENSE-2.0) for details.

## 🙏 THE DAILY BREAD

> "I am the way, and the truth, and the life; no one comes to the Father, but by me (JESUS)" — John 14:6
