# openWakeWord C++

C++ version of [openWakeWord](https://github.com/dscripka/openWakeWord).

## Build

1. Download a release of the [onnxruntime](https://github.com/microsoft/onnxruntime) and extract to `lib/<arch>` where `<arch>` is `uname -m`.
2. Run `make`


## Run

After building, run:

``` sh
arecord -r 16000 -c 1 -f S16_LE -t raw - | \
  build/openwakeword --model models/alexa_v0.1.onnx
```

You can add multiple `--model <path>` arguments. See `--help` for more options.


## Run on Mac

arecord is unavailable on Mac, so use the alternative `rec` instead.
Install `rec`: 
```
  brew install sox
```

Meantime, you need to specify the DYLD_LIBRARY_PATH so the `build/openwakeword` can locate the `libonnxruntime.1.17.1.dylib`.
```
  export DYLD_LIBRARY_PATH=$PWD/build:$DYLD_LIBRARY_PATH
```

After these two steps, run this command below to test out the onnx model:
```
  rec -r 16000 -c 1 -e signed-integer -b 16 -t raw - | \
  build/openwakeword --model models/hey_mycroft_v0.1.onnx
```
