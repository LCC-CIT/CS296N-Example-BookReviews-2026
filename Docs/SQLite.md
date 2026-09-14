# SQLite in BookReviews Project

## Overview

SQLite is integrated into the BookReviews project to provide flexibility for both application development and testing. This document explains how SQLite is configured and used in both contexts.

## SQLite in the Main Application

### How It Was Added

SQLite support is enabled through the Entity Framework Core NuGet package:
- **Package**: `Microsoft.EntityFrameworkCore.Sqlite`

This package provides the necessary database provider and native SQLite libraries for .NET applications.

### Configuration via Conditional Compilation

The application uses C# preprocessor directives (`#if` and `#undef`) to conditionally select between SQLite and MySQL databases at compile time.

**In `Program.cs`:**

```csharp
#undef SQLITE // use SQLite if this is #define, use MySQL if it's #undef
```

- **When `#define SQLITE`** is set: The application uses SQLite with a connection string from `appsettings.json` (`SqliteConnection`)
- **When `#undef SQLITE`** is set (default): The application uses MySQL with credentials from User Secrets (`DbUsername` and `DbPassword`)

#### Switching Between Databases

To switch from MySQL to SQLite:
1. Change the first line in `Program.cs` from `#undef SQLITE` to `#define SQLITE`
2. Rebuild the project
3. Run the application

### SQLite Connection Configuration

When SQLite is enabled:

```csharp
#if SQLITE
var connectionString = builder.Configuration.GetConnectionString("SqliteConnection");
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlite(connectionString));
#endif
```

The connection string should be defined in `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "SqliteConnection": "Data Source=BookReviews.db"
  }
}
```

## SQLite in Testing

### In-Memory Database for Unit Tests

The test project (`BookReviewTests`) uses SQLite's in-memory database capability for fast, isolated unit testing. This approach avoids the overhead of file I/O and ensures test data doesn't persist between test runs.

### Test Setup

**In `SetupTestRepo.cs`:**

```csharp
public static ApplicationDbContext CreateContext()
{
    var options = SqliteInMemory.CreateOptions<ApplicationDbContext>();
    return new ApplicationDbContext(options);
}
```

The `SqliteInMemory.CreateOptions<T>()` method (from the `EfCore.TestSupport` NuGet package) configures an in-memory SQLite database that:
- Exists only for the duration of the test
- Requires no file system access
- Is automatically destroyed after the test completes
- Provides a clean, isolated database state for each test

### Test Project Dependencies

The test project includes:
- **`Microsoft.EntityFrameworkCore.Sqlite`**: Provides SQLite database provider
- **`EfCore.TestSupport`**: Provides helper methods like `SqliteInMemory.CreateOptions<T>()` for easy in-memory database setup

## Advantages and Disadvantages

### SQLite in Application

#### Pros:
- **Zero Configuration**: No need to install or configure a separate database server
- **Single File**: Database is a single `.db` file, easy to backup and deploy
- **Low Overhead**: Minimal resource usage, ideal for development and small deployments
- **Cross-Platform**: Works identically on Windows, Linux, and macOS
- **Embedded**: Ships with your application; no external dependencies

#### Cons:
- **Limited Concurrency**: Not ideal for applications with high concurrent write loads
- **Scalability**: Less suitable for large datasets compared to enterprise databases
- **No Built-in Replication**: Lacks high-availability features of MySQL/PostgreSQL
- **Network Inaccessible**: Database is local to the application instance
- **Limited User Management**: No fine-grained permission system like enterprise databases

### SQLite In-Memory in Testing

#### Pros:
- **Speed**: No disk I/O overhead; tests run significantly faster
- **Isolation**: Each test gets a fresh, clean database state
- **No Cleanup**: In-memory databases are automatically destroyed; no manual cleanup needed
- **No Configuration**: Minimal setup required; works out of the box
- **Reproducible**: Same database schema and state for every test run

#### Cons:
- **Memory Usage**: Multiple in-memory databases can consume significant RAM in large test suites
- **Limited Size**: In-memory databases are limited by available system RAM
- **No Persistence**: Cannot inspect the database state after a test completes without exporting data
- **Different from Production**: May not catch database-specific issues that only occur with file-based SQLite or other database engines

## Summary

SQLite provides a lightweight, flexible solution for the BookReviews project:
- In the **main application**, it offers a simple alternative to MySQL for development and deployment
- In **testing**, it enables fast, isolated unit tests using in-memory databases
- **Preprocessor directives** make it easy to toggle between SQLite and MySQL at compile time without code changes

This approach is ideal for educational projects and small-to-medium applications where simplicity and ease of setup are priorities.
