# ffmpeg-cxc-build
Fast cross-compile ffmpeg for Windows with MinGW on Linux and Cygwin to produce a statically linked ffmpeg.

**Enabled Features**

amf aom ass/ssa bzip2 dav1d fdk-aac fontconfig freetype fribidi harfbuzz lame nvenc/nvdec ogg openssl opus png qsv sdl sofalizer theora vorbis vpx x264 x265 xml2 zlib

**Package Requirements**

Debian/Ubuntu/Mint:

sudo apt-get -y install autoconf automake build-essential cmake git-core gperf g++-mingw-w64 libtool mercurial meson nasm pkg-config python-lxml ragel subversion texinfo yasm wget
  
Fedora:

sudo yum install make autogen automake cmake gcc gcc-c++ git gettext-devel gperf kernel-devel libtool mercurial meson mingw64-gcc mingw64-gcc-c++ mingw64-winpthreads-static nasm python2-lxml ragel subversion uuid-devel yasm

Arch/Manjaro:

autoconf automake cmake git gperf libtool mercurial meson mingw-w64-binutils mingw-w64-crt mingw-w64-gcc mingw-w64-headers mingw-w64-tools mingw-w64-winpthreads nasm python-lxml ragel subversion wget yasm
  
Cygwin:
  
 After a baseline install, run setup and install the packages: autoconf autoconf2.1 autoconf2.5 autogen automake automake1.10 automake1.11 automake1.12 automake1.13 automake1.14 automake1.15 automake1.9 binutils cmake gcc-core gcc-g++ gettext gettext-devel gettext-doc git gperf libtool libuuid-devel make mercurial meson mingw64-x86_64-binutils mingw64-x86_64-gcc-core mingw64-x86_64-gcc-g++ mingw64-x86_64-gettext mingw64-x86_64-headers mingw64-x86_64-runtime mingw64-x86_64-win-iconv mingw64-x86_64-windows-default-manifest mingw64-x86_64-winpthreads nasm python27 python27-lxml python27-six ragel rsync subversion wget yasm
 
*Cygwin Preconditions:*
 
The mingw toolchain files must be in the path, and a link from the mingw sys-root directory to the sanbox build path must be created.  As an example, assuming the default configuration is used for the ROOT_PATH variable,  *ffmpeg-cxc-build-hints* has been placed in the user's home directory, and *ffmpeg-cxc-mingw64* is executable in the environment's path:
 
	ln -s /home /usr/x86_64-w64-mingw32/sys-root/home
	export PATH=$PATH:/usr/x86_64-w64-mingw32/sys-root/mingw/bin
	HINTS_FILE=~/ffmpeg-cxc-build-hints ffmpeg-cxc-mingw64

**Example Build Procedure**

Assumptions: ROOT_PATH is left to the default ($HOME) and *ffmpeg-cxc-mingw64* is executable in the environment's path.

	
	#fetch the source projects to the ~/src directory
	ROOT_PATH=~/ SRC_PATH=src HINTS_FILE=/dev/null CXC_FETCH_ONLY=1 ffmpeg-cxc-mingw64
	#copy ffmpeg-cxc-build-hints to ~/ and edit to fetch files from ~/src via URL override
	ffmpeg-cxc-mingw64
Using this technique, the script *update-repo* can be used to maintain up to date repositories by cd'ing into ~/src and running it.  Subsequent builds will then pull via the file URL override allowing up to date builds of ffmpeg and libraries if you edit the hints file and remove the commit hashes (empty means latest).  Note that fontconfig and openssl will likely require the hashes specified in the hints file to build and operate as expected.

**FFmpeg Latest Build Procedure**


	#using the ~/src directory as above - update and specify the path to ffmpeg-cxc-build-hints-file-head
	cd ~/src
	update-repo
	HINTS_FILE=~/ffmpeg-cxc-build-hints-file-head ffmpeg-cxc-mingw64

