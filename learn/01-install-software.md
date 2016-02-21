---
layout: default
---
# Install software

Before we start having fun let's make sure your development computer has the required software. There's only four things needed and you probably already have three covered.

## OpenGL

You'll need hardware and a device driver capable of OpenGL 3.3. If your video hardware was made after 2010 then you're probably fine. On Mac you'll get driver updates with the normal OS updates. Ubuntu distributes open source device drivers with their OS but you also have the option to install different, possibly better, proprietary drivers.

There's nothing for you to do here. However, in some rare cases you may run into problems because your video device driver is old or buggy. Just remember that programming OpenGL is programming direct to the device driver in case something weird comes up.

## Git

Git is required by the build system. If you have a Mac then you already have git installed. Git is used for the development of Linux so it's always going to be an easy install there. On Ubuntu you can make sure it's installed with the command `sudo apt-get install git`.

## Swift

Swift is freely available for both Linux and Mac. You can install a binary distribution or build it from source. The only Linux binaries that are officially being distributed are for Ubuntu. Other flavors of Linux can be used if you're willing to build from source, which is not trivial and not covered here. To keep things simple, we'll only be covering Ubuntu.

Start at the [Swift download page](https://swift.org/download/). The instructions there are accurate and detailed, so use them. I'll only include a brief summary here.

Make sure you download the Swift 2.2 Release Snapshot from January 11, 2016. This is the newest version known to work. Later versions of 2.2 do not include the package manager. All versions of 3.0 have a bug that make it incompatible with SwiftGL.
{: .alert .alert-danger}

For Mac, make sure you have met the requirements on the download page. Installation is an executable installer. Run it and let it do its thing. Don't forget that you need your PATH updated to find the executables from the command line.

For Ubuntu, you will need clang and libicu-dev installed. The distribution is a tar archive that you can unpack anywhere. Then update your PATH to find the executables from the command line.

## GLFW

OpenGL has no facility to open windows or create a context it can draw to. This is an intentional design choice and not an oversight. We'll be using GLFW, a cross-platform library, written in C, specifically targeted at OpenGL providing the bare necessities required for rendering goodies to the screen. It allows us to create an OpenGL context, define window parameters, and handle user input.

![Image of GLFW's logo](/images/glfw.png){:.img-rounded .pull-xs-right}{:width="192px" height="64px"}

If you have a Mac with homebrew, execute `brew install glfw3` in a terminal. That is all.

If you have a Mac with MacPorts, execute `sudo port install glfw` in a terminal. That is all.

If you're using Ubuntu, you'll need to install from source. You can also install from source on Mac if you aren't using a package manager. The GLFW documentation has specific information for both Ubuntu and OS X. Head on over to [Compiling GLFW](http://www.glfw.org/docs/latest/compile.html) to build GLFW from source.

Be sure to install GLFW version 3. Version 2 has a substantially different API and is still in many package managers.
{: .alert .alert-danger}
