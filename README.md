DigiByte API
===========

This is a C++ wrapper library for JSON-RPC communication with the DigiByte daemon. It allows developers to communicate with the DigiByte daemon without the need to pack and unpack JSON-RPC messages and thus simplifies the interaction with it.

Building the library
--------------------

[![Build Status](https://travis-ci.org/minium/digibyte-api-cpp.svg?branch=master)](https://travis-ci.org/minium/digibyte-api-cpp)

**Dependencies**

This library requires [CMake](http://www.cmake.org/cmake/resources/software.html), [Curl](http://curl.haxx.se/libcurl/), [libjson-cpp](https://github.com/open-source-parsers/jsoncpp) and [libjson-rpc-cpp](https://github.com/cinemast/libjson-rpc-cpp) packages in order to be built. All of them, with the exception of libjson-rpc-cpp, can be installed as follows

```sh
sudo apt-get install cmake libcurl4-openssl-dev libjsoncpp-dev
```

For the libjson-rpc-cpp library the instructions on [libjson-rpc-cpp](https://github.com/cinemast/libjson-rpc-cpp) must be followed.

**Build and install**

Navigate to the root directory of the library and proceed as follows:

```sh
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig
```

Using the library
-----------------
This example will show how the library can be used in your project. 

Filename getbalance.cpp

```
#include <digibyteapi/digibyteapi.h>

int main()
{
    std::string username = "user";
    std::string password = "pass";
    std::string address = "127.0.0.1";
    int port = 8332;

    try
    {
        /* Constructor to connect to the digibyte daemon */
        DigiByteAPI btc(username, password, address, port);

        /* Example method - getbalance */
        std::cout << "Wallet balance: " << btc.getbalance() << std::endl;
    }
    catch(DigiByteException e)
    {
        std::cerr << e.getMessage() << std::endl;
    }
}
```

To successfully compile the program you need to link it with the new library:
```
g++ getbalance.cpp -ldigibyteapi
```

The full list of available API calls can be found [here](https://developer.bitcoin.org/reference/rpc/). Nearly the complete list of calls is implemented and thoroughly tested.

License
-------

The digibyte-api-cpp library is released under the terms of [MIT](http://en.wikipedia.org/wiki/MIT_License).

```
Copyright (c) 2014 Krzysztof Okupski

Permission is hereby granted, free of charge, to any person obtaining a copy of 
this software and associated documentation files (the "Software"), to deal in the 
Software without restriction, including without limitation the rights to 
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of 
the Software, and to permit persons to whom the Software is furnished to do so, 
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all 
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, 
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR 
PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE 
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, 
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE 
OR OTHER DEALINGS IN THE SOFTWARE.
```

Used libraries
--------------
- [libjson-rpc-cpp](https://github.com/cinemast/libjson-rpc-cpp) C++ framework for JSON-RPC communication.

Acknowledgements
----------------
This code was base on the bitcoin-api-cpp [here](https://github.com/minium/bitcoin-api-cpp). However, the library was to old to still be useful.
