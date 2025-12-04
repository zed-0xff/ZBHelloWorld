# ZBHelloWorld

A simple example mod for [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) that demonstrates how to create a patches-only mod without requiring a main class.

## What It Does

This mod displays "Hello World from ZBHelloWorld!" text on the main menu screen by patching the game's `MainScreenState.renderBackground()` method.

## Features

- ✅ **Patches-only mod**: No main class required - demonstrates automatic patch discovery
- ✅ **Simple example**: Shows how to use `@Patch` annotations with ByteBuddy Advice
- ✅ **UI patching**: Demonstrates patching game UI rendering methods

## Installation

1. **Prerequisites**: You must have [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) installed and configured first
2. **Enable the mod**: Enable ZBHelloWorld in the Project Zomboid mod manager
3. **Launch the game**: You should see "Hello World from ZBHelloWorld!" text in the top-left corner of the main menu

## How It Works

This mod demonstrates a **patches-only** approach - it doesn't require a `javaMainClass` entry in `mod.info`. ZombieBuddy automatically scans the JAR file for `@Patch` annotated classes and applies them.

### mod.info Configuration

```ini
require=\ZombieBuddy
javaJarFile=media/java/client/build/libs/client.jar
```

Notice that there's no `javaMainClass` entry! ZombieBuddy will automatically discover the `@Patch` annotated class in the JAR.

### The Patch

```java
@Patch(className = "zombie.gameStates.MainScreenState", methodName = "renderBackground")
public class Patch_MainScreenState {
    @Advice.OnMethodExit
    public static void exit() {
        TextManager.instance.DrawString(UIFont.Medium, 0, 0, 
            "Hello World from ZBHelloWorld!", 1.0, 1.0, 1.0, 1.0);
    }
}
```

This patch:
- Targets the `renderBackground()` method in `MainScreenState`
- Uses `@Advice.OnMethodExit` to execute code after the method completes
- Draws text on the screen using the game's `TextManager`

## Building

1. Navigate to the Java project directory:
   ```bash
   cd 42/media/java/client
   ```

2. Build the JAR:
   ```bash
   ./gradlew build
   ```

3. The JAR will be created at `build/libs/client.jar`

## Project Structure

```
ZBHelloWorld/
├── 42/
│   ├── mod.info
│   └── media/
│       ├── java/
│       │   └── client/
│       │       ├── build.gradle
│       │       ├── src/
│       │       │   └── Patch_MainScreenState.java
│       │       └── build/
│       │           └── libs/
│       │               └── client.jar
│       └── lua/
│           └── client/
│               └── ZBHelloWorld.lua
└── README.md
```

## Learning Resources

This mod serves as a simple example for learning ZombieBuddy. For more information:

- **ZombieBuddy Framework**: See the [ZombieBuddy repository](https://github.com/zed-0xff/ZombieBuddy) for the framework source code and [detailed documentation](https://github.com/zed-0xff/ZombieBuddy/blob/master/README.md)
- **ByteBuddy Documentation**: Learn about [ByteBuddy Advice](https://bytebuddy.net/#/tutorial) for more advanced patching techniques

## Links

- **GitHub**: https://github.com/zed-0xff/ZBHelloWorld
- **ZombieBuddy Framework**: [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) - The framework this mod is built on

## License

See [LICENSE](LICENSE) file for details.

## Author

zed-0xff

