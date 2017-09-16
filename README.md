# Exploration 1: WebAssembly
David Auger

---
### About
This exploration is about setting up [WebAssembly](http://webassembly.org/) and learning how to use the [Emscripten LLVM](http://kripken.github.io/emscripten-site/index.html) to JavaScript compiler. WebAssembly allows you to write web apps in native C/C++ that runs at near native speeds.

**My git repo:** https://github.com/deayqf/WebAssembly.git

**My instance:** http://davidauger.tech/wasm/hello/

---
### Setup
**1. Open an SSH connectio with your EC2 instance and login.**

**2. Once you are in you home directory `user@host: ~ $` run these commands:**
  - These commands install the dependencies that Emscripten needs to build the SDK.
```bash
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install cmake
sudo apt-get install python2.7
sudo apt-get install nodejs
```
  - First we clone the [Emscripten repo](https://github.com/kripken/emscripten) and `cd` into it.
  - Then we install the latest version of the SDK and activate it for the current user, after that we source the file that starts the Emscripten LLVM compiler for the current terminal.
```bash
git clone https://github.com/kripken/emscripten.git
cd emsdk
./emsdk install latest
./emsdk activate latest
source ./emsdk_env.sh
```
**3. You now have the Emscripten compiler installed and running!**

---
### Hello World
**1. `cd` into your Apache document root:** `cd /var/www/html`

**2. Once you are in your document root, run these commands:**
  - `chmod 777` seems unnecessary but Emscripten has issues with permissions.
```bash
sudo mkdir hello
sudo chmod 777 hello
cd hello
```
**3. Now you are going to create a `hello.c` file: `sudo vim hello.c`**
  - The contents should look like this:
```c
#include <stdio.h>

int main( int argc, char** argv )
{
    printf( "Hello, World!\n" );
}
```
**4. When your file looks like mine, save and close the file and then run these commands:**
```bash
sudo chmod 777 hello.c
emcc hello.c -s WASM=1 -o index.html
```
  - If the compilation was successful there should be no output to the terminal, if you see a bunch of Python printed on the screen then re-run the `chmod 777` commands from above.

**5. If your file compiled then you can now go to your browser and navigate to your hello directory. You should see the Emscripten default page with a simulated terminal that says, "Hello, World!**
