#HSLIDE
# Hadoop Video Streaming
<hr>
#HSLIDE
###### Introduction
<hr>
- Unstructured Data
- About POT
- Video Streaming
#HSLIDE
###### Video Streaming
<hr>
**Two ways to play a video**
- Download to your local system
- Stream the video
#HSLIDE
###### Architecture For Streaming Video
<hr>
[![N|Solid](http://internetmemory.org/images/uploads/components.png)](http://internetmemory.org/images/uploads/components.png)
- The video file is split into fragments which are sent from the web server to the player, giving the illusion of a continuous stream
- We use **HDFS** to store the video
#HSLIDE
###### Problem
<hr>
- HDFS can in principle only be accessed through a Hadoop client, which the standard Apache server is not 
#HSLIDE
###### How ?
- How we can access the **HDFS** through a **Apache Server** ?
#HSLIDE
###### Solution
<hr>
**There are two ways**
1. Hoop - (Hadoop HDFS over HTTP ), provides REST like services. 
    * Streaming works, but seeking in an unbuffered part results in the playback stopping. 
2. Fuse
#HSLIDE
###### FUSE (Filesystem in Userspace)
<hr>
- Provided in Hadoop as a component named **“Mountable HDFS”**
- Allow HDFS to be mounted (on most flavors of Unix) as a standard file system 
- Can perform almost all Unix utilities such as 'ls', 'cd', 'cp', 'mkdir', 'find', 'grep' etc....

```sh
## In Hadoop
$ hadoop fs -ls /user/test

## In FUSE
$ ls -l /user/test
```

#HSLIDE
- Fuse consist of two components
    *  Fuse kernel module
    *  *libfuse* userspace library
- *libfuse* provides the reference implementation for communicating with the FUSE kernel module.
- The concept of **FUSE** is to create a simple kernel module that interacts with the kernel, particularly the VFS, on behalf of non-privileged user applications and has an API that can be accessed from userspace.
#HSLIDE
###### FUSE Architecture
<hr>
[![N|Solid](http://www.linux-mag.com/s/i/articles/7814/FUSE_structure.png)](http://www.linux-mag.com/s/i/articles/7814/FUSE_structure.png)
#HSLIDE
- The illustration corresponds to the “hello world” file system
- At a high level the “hello world” file system is compiled to create a binary called “hello”
- This binary is executed with a file system mount point of **/tmp/fuse**
#HSLIDE
- If the user executes an ls -l command against the mount point **(ls -l /tmp/fuse)**
    * Commands goes through glibc to the VFS
    * The VFS then goes to the FUSE module since the mount point corresponds to a FUSE based file system.
    * The FUSE kernel module then goes through glibc and libfuse and contacts the actual file system binary (“hello”)
    * The file system binary returns the results back down the stack

#VSLIDE
###### Virtual File System (VFS)
<hr>
- Abstraction layer on top of a more concrete file system
- The purpose of a VFS is to allow client applications to access different types of concrete file systems in a uniform way
-  A VFS can, for example, be used to access local and network storage devices transparently without the client application noticing the difference
#VSLIDE
-  It can be used to bridge the differences in Windows, classic Mac OS/macOS and Unix filesystems, so that applications can access files on local file systems of those types without having to know what type of file system they are accessing

[![N|Solid](https://upload.wikimedia.org/wikipedia/commons/e/e1/Operating_system_placement.svg)](https://upload.wikimedia.org/wikipedia/commons/e/e1/Operating_system_placement.svg)

#HSLIDE
###### Apache Server Configuration
<hr>
- To access the mounted FUSE system and load content from video files
- Streaming video content depends on the video format
- For mp4 video, we can use **H264 Streaming Module**, an apache plugin, which enables adaptive streaming

#HSLIDE
###### Unresolved Challenges
<hr>
- Finding streaming codec for **.AVI** format
- Testing the video streaming in cluster

#HSLIDE
###### Conclusion
<hr>
- The solution based on Apache + Mountable HDFS (FUSE) is
    * Simple and easy to set up
    * Functionally adequate (seeking is well supported)
    * Combine the benefits of HDFS and standard Web server streaming solutions
#HSLIDE
###### Thank you
<hr>
