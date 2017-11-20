# Hadoop Video Streaming
<hr>
# Introduction
- Unstructured Data
- About POT
- Video Streaming
<hr>
# Video Streaming
### Two ways to play a video
- Download to your local system
- Stream the video
<hr>
# Architecture For Streaming
[![N|Solid](http://internetmemory.org/images/uploads/components.png)](http://internetmemory.org/images/uploads/components.png)
- The video file is split into fragments which are sent from the web server to the player, giving the illusion of a continuous stream
- We use **HDFS** to store the video
<hr>
# Problem
- HDFS can in principle only be accessed through a Hadoop client, which the standard Apache server is not 
<hr>
### How ?
- How we can access the **HDFS** through a **Apache Server** ?
<hr>
# Solution
### There are two ways
1. Hoop - (Hadoop HDFS over HTTP ), provides REST like services. 
    * Streaming works, but seeking in an unbuffered part results in the playback stopping. 
2. Fuse
<hr>
# FUSE (Filesystem in Userspace)
- Provided in Hadoop as a component named **“Mountable HDFS”**
- Allow HDFS to be mounted (on most flavors of Unix) as a standard file system 
- Can perform almost all Unix utilities such as 'ls', 'cd', 'cp', 'mkdir', 'find', 'grep' etc....

