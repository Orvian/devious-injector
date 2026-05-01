# Devious Injector

A Gradle plugin for injecting code into RuneLite clients. This plugin transforms deobfuscated RuneLite bytecode by injecting custom hooks, mixins, and modifications.

## Purpose

The Devious Injector is used to:
- Inject API methods and hooks into the RuneLite client
- Apply mixins to modify client behavior
- Transform deobfuscated bytecode to include custom functionality
- Generate an injected client JAR ready for use

## Dependencies

- **Deobfuscator**: `net.unethicalite:deobfuscator:1.0.20-SNAPSHOT` (or STABLE)
- **ASM**: `org.ow2.asm:asm:9.0`
- **Guava**: `com.google.guava:guava:30.1.1-jre`
- **Kotlin**: `1.8.0`

## Building

To build the injector plugin:

```bash
./gradlew build
```

To publish to your local Maven repository:

```bash
./gradlew publishToMavenLocal
```

## Usage

### In a Gradle Project

Add the plugin to your `build.gradle.kts`:

```kotlin
plugins {
    id("com.openosrs.injector") version "2.0.30"
}
```

Add the repositories:

```kotlin
repositories {
    mavenLocal()
    maven {
        url = uri("https://raw.githubusercontent.com/Orvian/devious-artifacts/master")
    }
}
```

### Running the Inject Task

The plugin provides an `inject` task that:

1. Takes the deobfuscated client JAR
2. Applies injections and mixins
3. Outputs the injected client as `injected-client.oprs`

Run it with:

```bash
./gradlew inject
```

Or it runs automatically after the `assemble` task.

### Configuration

The injector can be configured via the `injector` extension:

```kotlin
injector {
    // Configuration options
}
```

## Project Structure

```
src/main/kotlin/com/openosrs/injector/
├── InjectPlugin.kt      # Main Gradle plugin entry point
├── InjectExtension.kt   # Configuration extension
└── Inject.kt           # Inject task implementation
```

## Publishing

To publish a new version:

1. Update version in `build.gradle.kts`
2. Build and publish:
   ```bash
   ./gradlew publishToMavenLocal
   ```
3. Copy artifacts to devious-artifacts repository
4. Commit and push devious-artifacts

## Version

Current version: `2.0.30`

