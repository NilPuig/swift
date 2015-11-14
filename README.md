# Swift Programming Language

**Welcome to Swift!**

Swift is a high performance systems programming language.  It has a clean
and modern syntax, and offers seamless access to existing C and Objective-C code
and frameworks, and is memory safe (by default).

Although inspired by Objective-C and many other languages, Swift is not itself a
C-derived language. As a complete and independent language, Swift packages core
features like flow control, data structures, and functions, with high-level
constructs like objects, protocols, closures, and generics.  Swift embraces
modules, eliminating the need for headers and the code duplication they entail.


## Documentation

To read the documentation, start by installing the Sphinx documentation
generator tool (http://sphinx-doc.org, just run `easy_install -U Sphinx` from
the command line and you're good to go).  Once you have that, you can build the
swift documentation by going into `swift/docs` and typing `make`.  This compiles
the 'rst' files in the docs directory into HTML in the `swift/docs/_build/html`
directory.

Once built, the best place to start is with the swift whitepaper, which gives a
tour of the language (in `swift/docs/_build/html/whitepaper/index.html`).
Another potentially useful document is `docs/LangRef`, which gives a low level
tour of how the language works from the implementation perspective.

Many of the docs are out of date, but you can see some historical design
documents in the `docs` directory.

Another source of documentation is the standard library itself, located at
`swift/stdlib`.  Much of the language is actually implemented in the library
(including `Int`), and the standard library gives some examples of what can be
expressed today.


## Getting Started

These instructions give the most direct path to a working Swift
development environment.  Options for doing things differently are
discussed below.


### System Requirements

OS X, Ubuntu Linux LTS, and the latest Ubuntu Linux release are the current
supported host development operating systems.

For OS X, you need [the latest Xcode](https://developer.apple.com/xcode/downloads/).

For Ubuntu, you'll need the following development dependencies:

    sudo apt-get install git cmake ninja-build clang uuid-dev libicu-dev libbsd-dev libedit-dev libxml2-dev libsqlite3-dev swig libpython-dev libncurses5-dev pkg-config

Note: LLDB currently requires at least swig-1.3.40 but will successfully build
with version 2 shipped with Ubuntu.


### Getting Sources for Swift and Related Projects

     git clone git@github.com:/apple/swift.git swift
     git clone git@github.com:/apple/swift-llvm.git llvm
     git clone git@github.com:/apple/swift-clang.git clang
     git clone git@github.com:/apple/swift-lldb.git lldb
     git clone git@github.com:/apple/swift-cmark.git cmark
     git clone git@github.com:/apple/swift-llbuild.git llbuild
     git clone git@github.com:/apple/swift-package-manager.git swiftpm


[CMake](http://cmake.org) is the core infrastructure used to configure builds of
Swift and its companion projects; at least version 2.8.12.2 is required. Your
favorite Linux distribution likely already has a CMake package you can install.
On OS X, you can download the [CMake Binary Distribution](https://cmake.org/install),
bundled as an application, copy it to /Applications, and add the embedded
command line tools to your `PATH`:

    export PATH=/Applications/CMake.app/Contents/bin:$PATH

[Ninja](http://martine.github.io/ninja/) is the current recommended build system
for building Swift and is the default configuration generated by CMake. If
you're on OS X or don't install it as part of your Linux distribution, clone
it next to the other projects and it will be bootstrapped automatically:

    git clone git@github.com:martine/ninja.git

You can also use a third-party packaging tool like [Homebrew](http://brew.sh) to
install the CMake and Ninja on OS X:

    brew install cmake ninja

### Building Swift

The `build-script` is a high-level build automation script that supports basic
options such as building a Swift-compatible LLDB, building the Swift Package
Manager, building for iOS, running tests after builds, and more. It also
supports presets which you can define for common combinations of build options.

To find out more:

    swift/utils/build-script -h

Note: Arguments after "--" above are forwarded to `build-script-impl`, which is
the ultimate shell script that invokes the actual build and test commands.

A basic command to build Swift and run basic tests with Ninja:

    swift/utils/build-script -t

## Develop Swift in Xcode

The Xcode IDE can be used to edit the Swift source code, but it is not currently
fully supported as a build environment for SDKs other than OS X. If you'd like
to build for other SDKs but still use Xcode, once you've built Swift using Ninja
or one of the other supported CMake generators, you can set up an IDE-only Xcode
environment using the build-script's `-X` flag:

    swift/utils/build-script -X --skip-build -- --reconfigure

The `--skip-build` flag tells build-script to only generate the project,
not build it in its entirety. A bare minimum of LLVM tools will build in order
to configure the Xcode projects.

The `--reconfigure` flag tells build-script-impl to run the CMake configuration
step even if there is a cached configuration. As you develop in Xcode, you may
need to rerun this from time to time to refresh your generated Xcode project,
picking up new targets, file removals, or file additions.

## Testing Swift

See docs/Testing.rst.
