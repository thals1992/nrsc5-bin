## Building on Fedora

Follow the Ubuntu instructions above, but replace the first command with the following:

    $ sudo dnf install make patch cmake autoconf libtool libao-devel fftw-devel rtl-sdr-devel libusb-devel

## Building on macOS using [Homebrew](https://brew.sh)

    $ curl https://raw.githubusercontent.com/theori-io/nrsc5/master/nrsc5.rb > /tmp/nrsc5.rb
    $ brew install --HEAD -s /tmp/nrsc5.rb

## Building for Windows

To build the program for Windows, you can either use [MSYS2](http://www.msys2.org) on Windows, or else use a cross-compiler on an Ubuntu, Debian or macOS machine. Scripts are provided to help with both cases.

### Building on Windows with MSYS2

Install [MSYS2](http://www.msys2.org). Open a terminal using the "MSYS2 MinGW 32-bit" shortcut. (Or use the 64-bit shortcut if you prefer a 64-bit build.)

    $ pacman -Syu

If this is the first time running pacman, you will be told to close the terminal window. After doing so, reopen using the same shortcut as before.

    $ pacman -Su
    $ pacman -S git
    $ git clone https://github.com/theori-io/nrsc5.git
    $ nrsc5/support/msys2-build

You can test your installation using the included sample file:

    $ cd ~/nrsc5/support
    $ xz -d sample.xz
    $ nrsc5.exe -r sample 0

If the sample file does not work, make sure you followed all of the instructions. If it still doesn't work, file an issue with the error message. Please put "[Windows]" in the title of the issue.

Once everything is built, you can run nrsc5 independently of MSYS2. Copy the following files from your MSYS2/mingw32 directory (e.g. C:\\msys64\\mingw32\\bin):

* libnrsc5.dll
* nrsc5.exe

### Cross-compiling for Windows from Ubuntu / Debian

    $ sudo apt install mingw-w64
    $ support/win-cross-compile 32

Replace `32` with `64` if you want a 64-bit build. Once the build is complete, copy `*.dll` and `nrsc5.exe` from the `build-win32/bin` (or `build-win64/bin`) folder to your Windows machine.

### Cross-compiling for Windows from macOS

    $ brew install mingw-w64
    $ support/win-cross-compile 32

Replace `32` with `64` if you want a 64-bit build. Once the build is complete, copy `*.dll` and `nrsc5.exe` from the `build-win32/bin` (or `build-win64/bin`) folder to your Windows machine.
