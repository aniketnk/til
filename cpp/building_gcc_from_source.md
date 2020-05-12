# Building GCC from source
> Fri May  8 02:36:29 IST 2020

GCC 10 released on 07-May-2020, and I was excited to test it out.  
I had to build it from source since none of the package managers had GCC 10.1 available. You can use the steps if you want to build the latest release from source, or even try any older version.  
This was tested on macOS Catalina, but the instructions should work the same with other GNU/Linux systems too!

Note: The official instructions can be found [here](https://gcc.gnu.org/install/index.html), but I wish to demonstrate a friendlier way(without mentioning all the optional parameters) to install from source.

*Important: Building from source releases, requires you to already have a C++ compiler installed.*

## Steps Overview

1. Download the source
2. Collect pre-requisites
3. Configure
4. Build
5. Install

### 1. Downloading the source  

The easiest way to fetch gcc's source code is to clone the git repository. (Note: You will need to have git installed on your machine.)
```sh
git clone git://gcc.gnu.org/git/gcc.git gcc-10
git checkout releases/gcc-10
```

Alternatively, you can also download gcc from one of it's mirrors, and extract it. 
- mirrors: [https://gcc.gnu.org/mirrors.html](https://gcc.gnu.org/mirrors.html)
- Navigate to `releases/gcc-x.y.z/` and download the tar file.

### 2. Collecting pre-requisites

The source release comes with handy shell script to download pre-requisites. You may simply run the `contrib/download_prerequisites` script in the GCC source directory to set up everything.
```sh
cd gcc-10
./contrib/download_prerequisites
```

### 3. Configuring

Like most GNU software, GCC must be configured before it can be built. For this tutorial, we will only look at the configuration procedure for building it natively.  
GCC recommends that GCC be built into a separate directory from the sources which does not reside within the source tree. Hence, let's make a new directory called `gcc_build` which lies in the same directory that contains `gcc-10`. 
```
parent-dir
├── gcc-10
└── gcc_build
```
Once the directory is created, we need to `cd` into it, and call the `configure` script present in the `gcc-10/` source directory. 
```
cd gcc_build
../gcc-10/configure
```
There are multiple options you can specify during the 'configure' phase, but I've skipped it for brevity. Options can be found [here](https://gcc.gnu.org/install/configure.html). 

### 4. Building

After the configuration process, you will find that it has placed a `Makefile` in your build directory. To build, all we have to do is to run the make command.  
Note: You may change `2` to the number of cores present on your machine.
```
make -j 2 
```

This will take several hours to build. When you use `make` in multi-threaded mode, i.e. using the `-j` option, you may lose error messages due to other threads outputting beyond the error. In this case, omit the `-j x` option to debug the output. 

You can *optionally* test your build by following the guide [here](https://gcc.gnu.org/install/test.html). 

### 5. Installing

Once the source release is successfully built, it is time to move the binaries to it's right location (somewhere in `$PATH`) so we can invoke it from the shell without it's full path.

Just the run the following command to install the binaries in `/usr/local` directory. This is the default installation directory prefixed during the 'configure' phase. 
```
cd gcc_build && make install
```

### Running

To check if gcc has properly installed, run the `gcc -v` command to see if the right gcc version was installed.  
![Screenshot](https://i.imgur.com/FywTc9m.png)
Make sure `/usr/local/bin` is present in your `$PATH`. 

## Conclusion
I hope this article helped you in building GCC from source. Please reach out if you run into any problems you can't figure out!
