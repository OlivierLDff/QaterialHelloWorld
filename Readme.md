# 👋 Qaterial HelloWorld

![image](https://user-images.githubusercontent.com/17255804/99988649-15512480-2db2-11eb-8f71-acd7515b3623.png)

Minimal code to start an application using [Qaterial](https://github.com/OlivierLDff/Qaterial). 

## Build & Execute

```bash
git clone https://github.com/OlivierLDff/QaterialHotReload
cd QaterialHotReload && mkdir build && cd build
cmake ..                # Configure
cmake --build .         # Build
./QaterialHelloWorld    # Execute
```

Make sure Qt5.15 can be found by `find_package`.
- Either pass `-DCMAKE_PREFIX_PATH=/path/to/Qt/5.15.1/<binary>`. `<binary>` can be `msvc2019_64`, `gcc_64`, `clang_64`, ...
- Or set environment variable `Qt5_DIR` to the same path.

## Author

Olivier Le Doeuff, [olivier.ldff@gmail.com](olivier.ldff@gmail.com)

## License

**QaterialHelloWorld** is available under the MIT license. See the [License](./License) file for more info.