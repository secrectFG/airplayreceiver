# AirPlay Receiver
Open source implementation of AirPlay 2 Mirroring / Audio protocol in C# .Net Core.  

## Generic

Tested on macOS with iPhone 12 Pro iOS14.  
  
The project is fully functional, but the AAC and ALAC libraries written in C ++ must be built.  
  
## How To

### Build AAC Codec
To download, build and install fdk-aac do the following:  
  
Clone the repository and cd into the folder:  
```
$ git clone https://github.com/mstorsjo/fdk-aac.git
$ cd fdk-aac
```
  
Configure the build and make the library:  
```
$ autoreconf -fi
$ ./configure
$ make
```
  
### Build ALAC Codec
To download, build and install alac do the following:  
  
Clone the repository and cd into the folder:  
```
$ git clone https://github.com/mikebrady/alac.git
$ cd alac
```
  
Download and paste 'GiteKat''s files in 'alac/codec' folder cloned before
```
$ https://github.com/GiteKat/LibALAC/tree/master/LibALAC
```
  
The 'mikebrady''s source code does not contains 'extern' keyword.
We need external linkage so we use 'GiteKat''s source code files.
  
<details>
<summary>
Edit makefile.original as follow
</summary>

```
# libalac make

CFLAGS = -g -O3 -c
LFLAGS = -Wall
CC = g++

SRCDIR = .
OBJDIR = ./obj
INCLUDES = .

HEADERS = \
$(SRCDIR)/EndianPortable.h \
$(SRCDIR)/aglib.h \
$(SRCDIR)/ALACAudioTypes.h \
$(SRCDIR)/ALACBitUtilities.h\
$(SRCDIR)/ALACDecoder.h \
$(SRCDIR)/ALACEncoder.h \
$(SRCDIR)/LibALAC.h \
$(SRCDIR)/dplib.h \
$(SRCDIR)/matrixlib.h

SOURCES = \
$(SRCDIR)/EndianPortable.c \
$(SRCDIR)/ALACBitUtilities.c \
$(SRCDIR)/ALACDecoder.cpp \
$(SRCDIR)/ALACEncoder.cpp \
$(SRCDIR)/LibALAC.cpp \
$(SRCDIR)/ag_dec.c \
$(SRCDIR)/ag_enc.c \
$(SRCDIR)/dp_dec.c \
$(SRCDIR)/dp_enc.c \
$(SRCDIR)/matrix_dec.c \
$(SRCDIR)/matrix_enc.c

OBJS = \
EndianPortable.o \
ALACBitUtilities.o \
ALACDecoder.o \
ALACEncoder.o \
LibALAC.o \
ag_dec.o \
ag_enc.o \
dp_dec.o \
dp_enc.o \
matrix_dec.o \
matrix_enc.o

libalac.a:	$(OBJS)
	ar rcs libalac.a $(OBJS)

EndianPortable.o : EndianPortable.c
	$(CC) -I $(INCLUDES) $(CFLAGS) EndianPortable.c

ALACBitUtilities.o : ALACBitUtilities.c
	$(CC) -I $(INCLUDES) $(CFLAGS) ALACBitUtilities.c

ALACDecoder.o : ALACDecoder.cpp
	$(CC) -I $(INCLUDES) $(CFLAGS) ALACDecoder.cpp

ALACEncoder.o : ALACEncoder.cpp
	$(CC) -I $(INCLUDES) $(CFLAGS) ALACEncoder.cpp

LibALAC.o : LibALAC.cpp
	$(CC) -I $(INCLUDES) $(CFLAGS) LibALAC.cpp

ag_dec.o : ag_dec.c
	$(CC) -I $(INCLUDES) $(CFLAGS) ag_dec.c

ag_enc.o : ag_enc.c
	$(CC) -I $(INCLUDES) $(CFLAGS) ag_enc.c

dp_dec.o : dp_dec.c
	$(CC) -I $(INCLUDES) $(CFLAGS) dp_dec.c

dp_enc.o : dp_enc.c
	$(CC) -I $(INCLUDES) $(CFLAGS) dp_enc.c

matrix_dec.o : matrix_dec.c
	$(CC) -I $(INCLUDES) $(CFLAGS) matrix_dec.c

matrix_enc.o : matrix_enc.c
	$(CC) -I $(INCLUDES) $(CFLAGS) matrix_enc.c
		
clean:
	-rm $(OBJS) libalac.a
```

</details>
  
<details>
<summary>
Edit makefile.am as follow
</summary>
  
```
## Copyright (c) 2013 Tiancheng "Timothy" Gu
## Modifications copyright (c) 2016 Mike Brady
## Licensed under the Apache License, Version 2.0 (the "License");
## you may not use this file except in compliance with the License.
## You may obtain a copy of the License at
## 
##     http://www.apache.org/licenses/LICENSE-2.0
## 
## Unless required by applicable law or agreed to in writing, software
## distributed under the License is distributed on an "AS IS" BASIS,
## WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
## See the License for the specific language governing permissions and
## limitations under the License.

lib_LTLIBRARIES = libalac.la

libalac_la_CPPFLAGS = -Wno-multichar
libalac_la_LDFLAGS = -version-info @ALAC_VERSION@

libalac_la_SOURCES = \
    EndianPortable.c \
    ALACBitUtilities.c \
    ALACDecoder.cpp \
    ALACEncoder.cpp \
    LibALAC.cpp \
    ag_dec.c \
    ag_enc.c \
    dp_dec.c \
    dp_enc.c \
    matrix_dec.c \
    matrix_enc.c

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = alac.pc

# Install to include/alac
alacincludedir = $(includedir)/alac

# Install everything
alacinclude_HEADERS = *.h
```

</details>

Configure the build and make the library:  
```
$ autoreconf -fi
$ ./configure
$ make
```
  
### Linux
On terminal type the follow to install build tools  
```
apt-get install build-essential autoconf automake libtool
```
Add compiled DLL path into 'appsettings_linux.json' file.  
  
### MacOS
On terminal type the follow to install build tools  

```
brew install autoconf automake libtool
```
Add compiled DLL path into 'appsettings_osx.json' file.  
  
### Windows

Use [this](http://www.gaia-gis.it/gaia-sins/mingw64_how_to.html#env) tutorial to understand how to install build tools and how to compile source code on Windows.  
You need MinGW32 or MinGW64 based on arch.  
  
Add compiled DLL path into 'appsettings_win.json' file.  
  
## Wiki
  
Here you will find an [Article](https://github.com/SteeBono/airplayreceiver/wiki) where I explain how the whole AirPlay 2 protocol works.
  
## Disclamier
  
All the resources in this repository are written using only opensource projects.  
The code and related resources are meant for educational purposes only.  
I do not take any responsibility for the use that will be made of it.    

## Credits

Inspired by others AirPlay open source projects.  
Big ty to OmgHax.c's author 😱. 

## If you want support me 🔥

If you appreciate my work, consider buying me a cup of coffee to keep me recharged 🥲  
  
BTC: 1MT4VAP3WnuNxSciWGAaasN9TxZiUPHtxv  
BCH: qp32ey3x9dc35up9ny3xzhprpwfmd8kclu65x3htl5  
ETH: 0xb2c39868d17eafccaadf516c8a306c240509c0a6  
