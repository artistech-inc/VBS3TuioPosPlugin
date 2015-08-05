#VBS3ZeroMqPosPlugin

This is a plugin for VBS3 for publishing a player's position data via [Google Buffer Protocol](https://developers.google.com/protocol-buffers/?hl=en) and [ZeroMq](http://zeromq.org/).

Currently builds for Visual Studio 2008 (x86 and x64).

##Installation
 1. Determine which DLL to use (x86 or x64).
 2. Download [pre-built dll](https://github.com/artistech-inc/VBS3ZeroMqPosPlugin/tree/v1.0/VBS3ZeroMqPosPlugin/bin).
 3. Place in C:\Bohemia Interactive\VBS3\plugins[64].
 4. Download the appropariate [ZeroMQ DLL](https://github.com/artistech-inc/VBS3ZeroMqPosPlugin/tree/v1.0/zeromq-4.0.4) for the target platform (x86 or x64).
 5. Download the appropariate [pthreads DLL](https://github.com/artistech-inc/VBS3ZeroMqPosPlugin/tree/v1.0/pthreads-2.9.1/lib) for the target platform (x86 or x64).
 6. These 2 DLLs must be placed in the Windows System PATH.
 7. Start VBS3
 8. Under Extensions, check that vbs3zeromqposplugin is loaded.

By default, the plugin is hard-coded to publish on port 5551.  If a different value is desired, the plugin must be recompiled with a different value hard-coded in.

##vbs3-pos-subscriber
This is a demo application for acting as a sink for listening to multiple VBS3ZeroMqPosPlugin instances and then publishing to multiple web-based clients.

###Requirements:
 1. Ubuntu
  1. sudo apt-get install libzmq3 libzmq3-dev libzmq-java
  2. Use of OpenJDK; if using Oracle Java,
   1. ln -s /usr/lib/jni/libjzmq.so /usr/lib/libjzmq.so
   2. ln -s /usr/lib/jni/libjzmq.so.0 /usr/lib/libjzmq.so.0
   3. ln -s /usr/lib/jni/libjzmq.so.0.0.0 /usr/lib/libjzmq.so.0.0.0
 2. OS X (untested), easier to configure the pom.xml file to use jeromq.
 3. Windows (untested), easier to configure the pom.xml file to use jeromq.

###Compile
 1. git clone https://github.com/artistech-inc/VBS3ZeroMqPosPlugin.git
 2. cd VBS3ZeroMqPosPlugin
 3. git checkout v1.0
 3. cd vbs3-pos-subscriber
 4. mvn clean package

###Run
By default, the JETTY_PORT_VALUE is 8888 unless otherwise specified on the command line.

java -jar target/vbs3-pos-subscriber-1.0.jar -z VBS3ZeroMqPosPlugin_SERVER_1:5551 -z VBS3ZeroMqPosPlugin_SERVER_2:5551 [-j JETTY_PORT_VALUE]

###Viewing
 1. Using the latest versions of Firefox and Google Chrome, view: http://vbs3-pos-subscriber_IP:JETTY_PORT_VALUE/vbs3_map.jsp
 2. Click "Start Receiving Data"
