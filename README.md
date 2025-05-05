# gsb
google starboard


## links

https://developers.google.com/youtube/cobalt/docs/development/setup-linux

https://github.com/youtube/cobalt

https://blog.csdn.net/weixin_43172485/article/details/86706512

## setup

```shell
sudo apt update && sudo apt install -qqy --no-install-recommends \
  bison clang libasound2-dev libgles2-mesa-dev libglib2.0-dev \
  libxcomposite-dev libxi-dev libxrender-dev nasm ninja-build \
  python3-venv

sudo apt install -qqy --no-install-recommends ccache

ccache --max-size=20G

# libglib2.0-dev : GLib is a general-purpose, portable utility library, which provides many useful data types, macros, type conversions, string utilities, file utilities, a mainloop abstraction, and so on.

# libasound2-dev: audio and MIDI functionality to the Linux operating system. A

# libgles2-mesa-dev: free implementation of the OpenGL|ES 2.x API -- development files
# OpenGL|ES is a cross-platform API for full-function 2D and 3D graphics on embedded systems - including consoles, phones, appliances and vehicles. It contains a subset of OpenGL plus a number of extensions for the special needs of embedded systems.
# OpenGL|ES 2.x provides an API for programmable hardware including vertex and fragment shaders.
# This package provides a development environment for building applications using the OpenGL|ES 2.x APIs.

# libxcomposite-dev: composition
# client library for the Composite extension to the X11 protocol
# The Composite extension causes a entire sub-tree of the window hierarchy to be rendered to an off-screen buffer. Applications can then take the contents of that buffer and do whatever they like. The off-screen buffer can be automatically merged into the parent window or merged by external programs, called compositing managers.


# libxi-dev: X11 Input extension library (development headers)
# libXi provides an X Window System client interface to the XINPUT extension to the X protocol.
# The Input extension allows setup and configuration of multiple input devices, and hotplugging of input devices (to be added and removed on the fly).
# This package contains the development headers for the library found in libxi6. Non-developers likely have little use for this package.


# libxrender-dev: The X Rendering Extension (Render) introduces digital image composition as the foundation of a new rendering model within the X Window System. Rendering geometric figures is accomplished by client-side tessellation into either triangles or trapezoids. Text is drawn by loading glyphs into the server and rendering sets of them. The Xrender library exposes this extension to X clients. This package provides a static library and C header files.

# nsam: assembler: assembly programming, you’ll require a reliable assembler.
# Installing NASM and Writing Your First Assembly Program on Linux
# NASM, short for “Netwide Assembler“, is a widely used software tool in computer programming. It transforms assembly language code into executable machine code, or binary code, for a computer’s CPU.


https://cs.lmu.edu/~ray/notes/nasmtutorial/?ref=linuxtldr.com

whereis nasm
sudo apt install nasm 
nasm --version


# install GN
#N is a meta-build system that generates build files for Ninja.


# update .bashrc 

export PYTHONPATH="/home/github.com/xcheng85/cobalt:${PYTHONPATH}"
export COBALT_SRC="/home/github.com/xcheng85/cobalt"

python3 -m venv ~/.virtualenvs/cobalt_dev
source ~/.virtualenvs/cobalt_dev/bin/activate
pip install -r requirements.txt

./starboard/tools/download_clang.sh

#downloaded to /home/xcheng85/starboard-toolchains/x86_64-linux-gnu-clang-chromium-17-init-8029-g27f27d15-3
```

## Build gn tool from source

```shell

# generate out folder which container build.ninja
python build/gen.py
# compile the configs in out folder
ninja -C out
# where to look for the gn
../../out/gn gen -C out
```

## Build Cobalt
```shell
# The current repo is not first on the PYTHONPATH.


Ubuntu Linux, the canonical platform is linux-x64x11.

command-line flag to specify a build_type. Valid build types are debug, devel, qa, and gold

python cobalt/build/gn.py -c debug -p linux-x64x11

python cobalt/build/gn.py 

# symbolic link for python
sudo apt-get install -y python-is-python3

# python script will create out folder

# """Thin wrapper for building Starboard platforms with GN."""
cobalt/cobalt/build/build.py
cobalt/starboard/build/platform.py

# all the starboard platforms

PLATFORMS = {
    'stub': 'starboard/stub',
    'linux-x64x11': 'starboard/linux/x64x11',
    'linux-x64x11-egl': 'starboard/linux/x64x11/egl',
    'linux-x64x11-gcc-6-3': 'starboard/linux/x64x11/gcc/6.3',
    'linux-x64x11-skia': 'starboard/linux/x64x11/skia',
    'linux-x64x11-clang-3-9': 'starboard/linux/x64x11/clang/3.9',
    'android-arm': 'starboard/android/arm',
    'android-arm64': 'starboard/android/arm64',
    'android-arm64-vulkan': 'starboard/android/arm64/vulkan',
    'android-x86': 'starboard/android/x86',
    'raspi-2': 'starboard/raspi/2',
    'raspi-2-skia': 'starboard/raspi/2/skia',
    'rdk-arm': 'starboard/contrib/rdk/src/third_party/starboard/rdk/arm',
    'evergreen-x64': 'starboard/evergreen/x64',
    'evergreen-arm-hardfp': 'starboard/evergreen/arm/hardfp',
    'evergreen-arm-softfp': 'starboard/evergreen/arm/softfp',
    'evergreen-arm64': 'starboard/evergreen/arm64',
    'win-win32': 'starboard/win/win32',
    'xb1': 'starboard/xb1',
}

# in gn.py, you will the argument parser as 

parser.add_argument

## default build directory is out
    builds_directory = os.getenv('COBALT_BUILDS_DIRECTORY',
                                 script_args.builds_directory or 'out')
## check this command
  gn_command = [
      'gn', f'--script-executable={sys.executable}', 'gen', out_directory
  ] + gn_gen_args
  print(' '.join(gn_command))


python cobalt/build/gn.py -c debug -p linux-x64x11

# out/linux-x64x11_debug/args.gn already exists. Running ninja will regenerate build files automatically.
# gn --script-executable=/home/xcheng85/.virtualenvs/cobalt_dev/bin/python gen out/linux-x64x11_debug --check

# https://chromium.googlesource.com/chromium/src/+/64edbcf758a9c60fbd1679460e1fd69db29998f7/tools/gn/docs/reference.md

# --script-executable: Set the executable used to execute scripts.
#   By default GN searches the PATH for Python to execute scripts in
#   action targets and exec_script calls. This flag allows the
#   specification of a specific Python executable or potentially
#   a different language interpreter.


# debug, devel, qa, and gold
# build cobalt
ninja -C out/linux-x64x11_debug cobalt
# build glclear
ninja -C out/linux-x64x11_debug starboard_glclear_example

ninja -C out/linux-x64x11_debug starboard_window_example
ninja -C out/linux-x64x11_debug starboard_hello_world_example
ninja -C out/linux-x64x11_debug extension_test
#run test case
ninja -C out/linux-x64x11_debug nplb


    "//starboard/client_porting/cwrappers:cwrappers_test",
    "//starboard/client_porting/eztime:eztime_test",
    "//starboard/client_porting/icu_init",

    "//starboard/examples/glclear:starboard_glclear_example",
    "//starboard/examples/hello_world:starboard_hello_world_example",
    "//starboard/examples/window:starboard_window_example",
    "//starboard/extension:extension_test",
    "//starboard/nplb",


label_name = starboard_glclear_example
target_out_dir = obj/starboard/examples/glclear
target_output_name = starboard_glclear_example

# 
```