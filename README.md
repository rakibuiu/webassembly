# webassembly
playing with webassembly

## Getting started

This simple documentation is nothing more than a summary of the atual documentation, found at http://webassembly.org/getting-started/developers-guide/

My environment is a PC running Linux Mint. For details about Mac or Windows, please go to the oficial web site and check the documentation mentioend above.

## Live Sample

http://williancarvalho.com/webassembly/

## Requirements
 * Git
 * Cmake
 * Python 2.7.x
 * GCC

## Steps

### Compile Emscripten

  **Warning:** This step takes forever. If you don't have much time, don't even start this. Specially if you need to install all required tools. Seriously, it took around 3 hours to build the thing.

        $ git clone https://github.com/juj/emsdk.git
        $ cd emsdk
        $ ./emsdk install sdk-incoming-64bit binaryen-master-64bit
        $ ./emsdk activate sdk-incoming-64bit binaryen-master-64bit

### Enter an Emscripten compiler environment

        $ source ./emsdk_env.sh

### Write a C code

```c
      #include <stdio.h>

      int main (int argc, char ** argv) {
        char * hello = "Hello, Webassembly!";
        printf("%s\n", hello);
      }
```

### Compile it with emcc

        emcc hello.c -s WASM=1 -o hello.html

This command will output an HTML page, a Javascript file and a WASM file

### Start a webserver and call `hello.html`

        python -m SimpleHTTPServer

That's that!

### Being lazy

If you happen to have a very similar environment as mine, you can use my `Makefile` to do the job for you:

        $ make

This will build the 3 files into a `dist` folder.

To be even lazier, you can run

        $ make .serve_web

Which will build stuff to the `dist` folder and start the Python SimpleHTTPServer. Then go to `http://localhost:8000/dist` to see the page.

To be extremely super lazy, just see the results at http://williancarvalho.com/webassembly/