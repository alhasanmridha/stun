STUN
---------------------------------------------------------
A C++ STUN client for getting NAT type and external IP

This is the cmake version of [stunserver] (https://github.com/jselbie/stunserver) originally created by jselbie.
  Compliant with the latest RFCs including 5389, 5769, and 5780. Also includes
  backwards compatibility for RFC 3489.

  Supports both UDP and TCP on both IPv4 and IPv6.

  Client test app provided.

  Stun server can operate in "full" mode as well as "basic" mode. Basic mode
  configures the server to listen on one port and respond to STUN binding
  requests. Full mode configures the service to listen on two different IP
  address interfaces (if available) and provide NAT behavior and filtering
  detection support for clients.

  Support for running a full mode STUN service on an Amazon EC2 instance. Run
  "stunserver --help" for visit www.stunprotocol.org on how to configure this
  mode.

  Open source Apache license. See LICENSE file fore more details.

##### Known issues:

  TLS mode has yet to be implemented.

  Server does not honor the stun padding attribute. If someone really wants
  this support, let me know and I will consider adding it.

  By default, the stun server operates in an open mode without performing
  authentication. All the code for authentication, challenge-response, message
  hashing, and message integrity attributes are fully coded. HMAC/SHA1/MD5
  hashing code for generating and validating the message integrity attribute
  has been implemented and tested. However, the code for validating a username
  or looking up a password is outside the scope of this release. Instead,
  hooks are provided for implementors to write their own code to validate a
  username, fetch a password, and allow/deny a request. Details of writing
  your own authentication provider code are described in the file
  "server/sampleauthprovider.h".

##### Testing:

  Fedora 15 with gcc/g++ 4.6.0
  Fedora 17 with gcc/g++ 4.72
  Ubuntu 11 with gcc/g++ 4.5.2
  Ubuntu 12 with gcc/g++ 4.6.3
  Ubuntu 12 with clang/clang++ 3.0
  Amazon AWS with gcc/g++ 4.4
  MacOS with XCode 7 and command line tools
  FreeBSD 9.0 with gcc/g++ 4.2.1
  Solaris 11 with gcc/g++ 4.5.2

  Parsing code has been fuzz tested with zzuf. http://caca.zoy.org/wiki/zzuf

Prerequisites before compiling and running.
---------------------------------------------

  The short summary is that you need a C++ compiler (g++ preferred or
  clang++), GNU make, Boost header files, and the OpenSSL development files in
  order to compile the code. Below are the set of package installer commands
  that you can type from the command line to get the tools and libraries you
  need.

  Debian/Ubuntu/Mint
  
  ```
  sudo apt-get install g++
  sudo apt-get install cmake
  sudo apt-get install libboost-dev # For Boost
  sudo apt-get install libssl-dev # For OpenSSL
```
  RedHat/Fedora and EC2 Amazon Linux AMI
  ```
  sudo yum groupinstall "Development Tools" # For g++, make, et. al.
  sudo yum install boost-devel # For Boost
  sudo yum install openssl-devel # For OpenSSL
```
  Solaris and Mac
  OpenSSL is already installed on Solaris and is not needed on Mac.

  ##### Manual Boost install
  The compiled Boost runtime is not necessary. Just obtaining and unpacking
    the Boost source code distribution from www.boost.org will suffice. If you
    do not have the adminstrative privaleges to install the Boost distribution
    into a standard system include path, you may uncomment and edit the top
    line of the common.inc file for the BOOST_INCLUDE variable. The common.inc
    file is in the same folder as this README file.

  ##### Manual OpenSSL install
You can obtain the OpenSSL development files and runtime from
    www.openssl.org. On most systems with development tools already installed,
    OpenSSL include files are already installed in the standard include path.
    If this is not the case, you can uncomment and edit the common.inc file to
    have the OPENSSL_INCLUDE variable defined.

  Other prerequisites
     pthreads and perl. I've never come across a system where this wasn't
     already pre-installed.

Compiling and running
----------------------
Got Boost and OpenSSL taken care of as described above? Good. Just type
```
cmake -H. -Bbuild
cmake --build build
```

The binaries will be created in respective directories inside build directory i.e location of the server will be build/server/.
  stuntestcode - This is the unit test code. I highly recommend you run this
  program first. When run, you'll see a series of lines being printed in
  regards to different code paths being tested. If you see any line that ends
  in "FAIL", we likely have a bug. Please contact me immediately if you see
  this.

  stunserver - this is the server binary. Run "./build/server/server --help" for
  details on running this program. Running this program without any command
  line arguments defaults to listening on port 3478 on all adapters.

  stunclient - this is the client test binary. Run "./build/client/client --help" for
  details on running this program. Example: "./build/client/client stun.l.google.com 19302"


Firewall

  Don't forget to configure your firewall to allow traffic for the local ports
  the stunserver will be listening on!


Feature roadmap (the features I want to implement in a subsequent release)

  Cleanup Makefile and add "configure" and autotools support

  Finish Windows port and able to run as a Windows service

  Scale across more than one CPU (for multi-core and multi-proc machines). The
  threading code has already been written, just needs some finish work.

  TLS support

Docker
```
docker image build -t=stun-server-image
docker container run -d -p 3478:3478/tcp -p 3478:3478/udp --name=stun-container stun-server-image
```

Contact the author
mdalhasanmridha@gmail.com


