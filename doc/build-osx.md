Mac OS X Build Instructions and Notes
====================================
The commands in this guide should be executed in a Terminal application.
The built-in one is located in `/Applications/Utilities/Terminal.app`.

Preparation
-----------
Install the OS X command line tools:

`xcode-select --install`

When the popup appears, click `Install`.

Then install [Homebrew](https://brew.sh).

Dependencies
----------------------

    brew install automake libtool boost miniupnpc openssl pkg-config protobuf qt5 libevent
    brew install berkeley-db # You need to make sure you install a version >= 5.1.29, but as close to 5.1.29 as possible. Check the homebrew docs to find out how to install older versions.

If you want to build the disk image with `make deploy` (.dmg / optional), you need RSVG

    brew install librsvg

NOTE: Building with Qt4 is still supported, however, could result in a broken UI. Building with Qt5 is recommended.

Build Draupnir Core
------------------------

1. Clone the draupnir source code and cd into `draupnir`

        git clone https://github.com/draupnir/draupnir
        cd draupnir

2.  Build draupnir:

    Configure and build the headless draupnir binaries as well as the GUI (if Qt is found).

    You can disable the GUI build by passing `--without-gui` to configure.

        ./autogen.sh
        ./configure
        make

3.  It is recommended to build and run the unit tests:

        make check

4.  You can also create a .dmg that contains the .app bundle (optional):

        make deploy

Running
-------

Draupnir Core is now available at `./src/draupnird`

Before running, it's recommended you create an RPC configuration file.

    echo -e "rpcuser=draupnirrpc\nrpcpassword=$(xxd -l 16 -p /dev/urandom)" > "/Users/${USER}/Library/Application Support/Draupnir/draupnir.conf"

    chmod 600 "/Users/${USER}/Library/Application Support/Draupnir/draupnir.conf"

The first time you run draupnird, it will start downloading the blockchain. This process could take several hours.

You can monitor the download process by looking at the debug.log file:

    tail -f $HOME/Library/Application\ Support/Draupnir/debug.log

Other commands:
-------

    ./src/draupnird -daemon # Starts the draupnir daemon.
    ./src/draupnir-cli --help # Outputs a list of command-line options.
    ./src/draupnir-cli help # Outputs a list of RPC commands when the daemon is running.

Using Qt Creator as IDE
------------------------
You can use Qt Creator as an IDE, for draupnir development.
Download and install the community edition of [Qt Creator](https://www.qt.io/download/).
Uncheck everything except Qt Creator during the installation process.

1. Make sure you installed everything through Homebrew mentioned above
2. Do a proper ./configure --enable-debug
3. In Qt Creator do "New Project" -> Import Project -> Import Existing Project
4. Enter "draupnir-qt" as project name, enter src/qt as location
5. Leave the file selection as it is
6. Confirm the "summary page"
7. In the "Projects" tab select "Manage Kits..."
8. Select the default "Desktop" kit and select "Clang (x86 64bit in /usr/bin)" as compiler
9. Select LLDB as debugger (you might need to set the path to your installation)
10. Start debugging with Qt Creator

Notes
-----

* Tested on OS X 10.8 through 10.12 on 64-bit Intel processors only.

* Building with downloaded Qt binaries is not officially supported. See the notes in [#7714](https://github.com/draupnir/draupnir/issues/7714)
