# ZBHelloWorld

A simple example mod for [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) that demonstrates how to create a patches-only mod without requiring a main class.

## ☕ Support the Developer

If you find this example helpful or enjoy using ZombieBuddy, consider supporting the developer with a coffee!

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/zed_0xff)

## What It Does

This mod displays "Hello World from ZBHelloWorld!" text on the main menu screen by patching the game's `MainScreenState.renderBackground()` method.

## Features

- ✅ **Patches-only mod**: No Main class required - demonstrates automatic patch discovery from package
- ✅ **Simple example**: Shows how to use `@Patch` annotations
- ✅ **UI patching**: Demonstrates patching game UI rendering methods

## Installation

1. **Prerequisites**: You must have [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) installed and configured first
2. **Enable the mod**: Enable ZBHelloWorld in the Project Zomboid mod manager
3. **Launch the game**: You should see "Hello World from ZBHelloWorld!" text in the top-left corner of the main menu

## How It Works

This mod demonstrates a **patches-only** approach - it doesn't require a Main class. ZombieBuddy automatically discovers and applies `@Patch` annotated classes from the package specified in `javaPkgName`.

### mod.info Configuration

```ini
require=\ZombieBuddy
javaJarFile=media/java/client/build/libs/client.jar
javaPkgName=me.zed_0xff.zb_hello_world
```

Notice that there's no Main class! The `javaPkgName` entry specifies the package where patches are located. ZombieBuddy will automatically discover and apply all `@Patch` annotated classes in that package.

### The Patch

```java
import me.zed_0xff.zombie_buddy.Patch;

@Patch(className = "zombie.gameStates.MainScreenState", methodName = "renderBackground")
public class Patch_MainScreenState {
    @Patch.OnExit
    public static void exit() {
        TextManager.instance.DrawString(UIFont.Medium, 0, 0, 
            "Hello World from ZBHelloWorld!", 1.0, 1.0, 1.0, 1.0);
    }
}
```

This patch:
- Targets the `renderBackground()` method in `MainScreenState`
- Uses `@Patch.OnExit` to execute code after the method completes
- Draws text on the screen using the game's `TextManager`

## Building

1. Navigate to the Java project directory:
   ```bash
   cd 42/media/java/client
   ```

2. Build the JAR:
   ```bash
   gradle build
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

## Links

- **GitHub**: https://github.com/zed-0xff/ZBHelloWorld
- **ZombieBuddy Framework**: [ZombieBuddy](https://github.com/zed-0xff/ZombieBuddy) - The framework this mod is built on

## License

See [LICENSE](LICENSE) file for details.

## Author

zed-0xff

