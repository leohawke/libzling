libzling
========

**fast and lightweight compression library and utility.**

Introduction
============

Libzling is an improved lightweight compression utility and library. libzling uses fast order-1 ROLZ (16MB block size and 10MB dictionary size) followed with Huffman encoding, making it **twice as fast as gzip on compressing, while still getting better compression ratio and decompression speed**.

Simple benchmark with **enwik8**(100,000,000 bytes)

Tool    | Compressed Size | Encode | Decode |
--------|-----------------|--------|--------|
zling d0| 33391KB         | 2.54s  | 1.13s  |
zling e1| 32614KB         | 2.90s  | 1.10s  |
zling d2| 31732KB         | 3.39s  | 1.08s  |
zling e3| 31310KB         | 3.95s  | 1.05s  |
zling e4| 30862KB         | 6.02s  | 1.03s  |
gzip    | 36520KB         | 8.13s  | 1.47s  |

Simple benchmark with **fp.log**(20,617,071 bytes)

Tool  | Compressed Size | Encode | Decode |
------|-----------------|--------|--------|
zling | 987KB           | 0.10s  | 0.07s  |
zling | 925KB           | 0.11s  | 0.07s  |
zling | 902KB           | 0.14s  | 0.07s  |
zling | 913KB           | 0.17s  | 0.07s  |
zling | 918KB           | 0.33s  | 0.07s  |
gzip  | 1449KB          | 0.41s  | 0.14s  |

Build & Install
===============

You can build and install libzling automatically by **cmake** with the following command:

    cd ./build
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/path/to/install
    make
    make install

Usage
=====

Libling provides simple and lightweight interface. here is a simple program showing the basic usage of libzling. (compiled with `g++ -Wall -O3 zling_sample.cpp -o zling_sample -lzling`)

```C++
#include "libzling/libzling.h"

int main() {
    // compress
    {
        FILE* fin = fopen("./1.txt", "rb");
        FILE* fout = fopen("./1.txt.zlng", "wb");

        baidu::zling::FileInputter  inputter(fin);
        baidu::zling::FileOutputter outputter(fout);

        baidu::zling::Encode(&inputter, &outputter);
        fclose(fin);
        fclose(fout);
    }

    // decompress
    {
        FILE* fin = fopen("./1.txt.zlng", "rb");
        FILE* fout = fopen("./2.txt", "wb");

        baidu::zling::FileInputter  inputter(fin);
        baidu::zling::FileOutputter outputter(fout);

        baidu::zling::Decode(&inputter, &outputter);
        fclose(fin);
        fclose(fout);
    }
    return 0;
}
```
However libzling supports more complicated interface, see **./demo/zling.cpp** for details.
