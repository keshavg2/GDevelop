# GDevelop.js

This is the port of GDevelop core classes to JavaScript. This allow [GDevelop Core libraries](https://github.com/4ian/GDevelop) to run in a browser or on Node.js.

> 🎮 GDevelop is a full featured, cross-platform, open-source game development software requiring no programming skills. Download it on [the official website](https://gdevelop-app.com).

## How to build

> 👋 Usually if you're working on GDevelop editor or extensions in JavaScript, you don't need rebuilding GDevelop.js. If you want to make changes in C++ extensions or classes, read this section.

- Make sure you have [CMake 3.5+](http://www.cmake.org/) and [Node.js](nodejs.org/) installed.

- Install [Emscripten](https://github.com/kripken/emscripten), as explained on the [Emscripten installation instructions](http://kripken.github.io/emscripten-site/docs/getting_started/downloads.html):

| Linux/macOS                                  | Windows                                      |
| -------------------------------------------- | -------------------------------------------- |
| `git clone https://github.com/juj/emsdk.git` | `git clone https://github.com/juj/emsdk.git` |
| `cd emsdk`                                   | `cd emsdk`                                   |
| `./emsdk update`                             | `emsdk update`                               |
| `./emsdk install 1.39.6`                     | `emsdk install 1.39.6`                       |
| `./emsdk activate 1.39.6`                    | `emsdk activate 1.39.6`                      |
| `source ./emsdk_env.sh`                      | `emsdk_env.bat`                              |

- Launch the build from GDevelop.js folder:

```shell
    cd GDevelop.js
    npm install
    npm run build
```

> ℹ️ Output is created in _/path/to/GD/Binaries/embuild/GDevelop.js/_ and also copied to GDevelop 5 IDE (`newIDE` folder).

> ⏱ As the linking (last step) of the build can be very long, you can run `npm run build -- --dev` to disable temporary optimizations and get a (slightly) faster build.

- You can then launch GDevelop 5 that will use your build of GDevelop.js:

```shell
    cd ..
    cd newIDE/app
    npm install
    npm start
```

More information in [GDevelop 5 readme](https://github.com/4ian/GD/blob/master/newIDE/README.md).

### Tests

```
npm test
```

### About the internal steps of compilation

The npm _build_ task:

- Creates `Binaries/embuild` directory,
- Launches CMake inside to compile GDevelop with _emconfigure_ to use Emscripten toolchain,
- Updates the glue.cpp and glue.js from Bindings.idl using _Emscripten WebIDL Binder_,
- Launches the compilation with `make` (or `ninja` on Windows).

See the [CMakeLists.txt](./CMakeLists.txt) for the arguments passed to the Emscripten linker.

## Documentation

- The file [Bindings.idl](https://github.com/4ian/GDevelop/blob/master/GDevelop.js/Bindings/Bindings.idl) describes all the classes available in GDevelop.js.
- Refer to [GDevelop documentation](https://docs.gdevelop-app.com/GDCore%20Documentation/) for detailed documentation of the original C++ classes.
