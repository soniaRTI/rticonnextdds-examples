===============================================================
 Example Code -- Content Filtered Topic - Using string filter
===============================================================

Building Java Example
=====================
Before compiling or running the example, make sure the environment variable 
NDDSHOME is set to the directory where your version of RTI Connext is installed.

Run rtiddsgen with the -example option and the target architecture of your 
choice (e.g., i86Win32VS2005 or i86Linux2.6gcc4.4.3). The RTI Connext Core 
Libraries and Utilities Getting Started Guide describes this process in detail. 
Follow the same procedure to generate the code and build the examples. Do not 
use the -replace option.

On Windows systems run:

rtiddsgen -language Java -example i86Win32jdk cft.idl

On UNIX systems (assuming you want to generate an example for 
i86Linux2.6gcc4.4.3) run:

rtiddsgen -language Java -example i86Linux2.6gcc4.4.3jdk cft.idl

You will see messages that look like this:

File C:\local\content_filtered_topic_string_filter\java\cftSubscriber.java 
already exists and will not be replaced with updated content. If you would like 
to get a new file with the new content, either remove this file or supply 
-replace option.
File C:\local\content_filtered_topic_string_filter\java\cftPublisher.java 
already exists and will not be replaced with updated content. If you would like 
to get a new file with the new content, either remove this file or supply 
-replace option.
File C:\local\content_filtered_topic_string_filter\java\USER_QOS_PROFILES.xml 
already exists and will not be replaced with updated content. If you would like 
to get a new file with the new content, either remove this file or supply 
-replace option.

This is normal and is only informing you that the subscriber/publisher code has 
not been replaced, which is fine since all the source files for the example are 
already provided.

Before compiling in Java, make sure that the desired version of the javac 
compiler is in your PATH environment variable.

On Windows systems run:

javac -classpath .;%NDDSHOME%\class\nddsjava.jar cft.java cftSeq.java cftTypeSupport.java cftTypeCode.java cftDataReader.java cftDataWriter.java cftSubscriber.java cftPublisher.java

On Unix systems (including Linux and MacOS X):

javac -classpath .:$NDDSHOME/class/nddsjava.jar cft.java cftSeq.java cftTypeSupport.java cftTypeCode.java cftDataReader.java cftDataWriter.java cftSubscriber.java cftPublisher.java

Running Java Example
====================
Before running, make sure that the native Java libraries on which RTI Connext
depends are in your environment path (or library path). To add Java libraries 
to your environment...

On Windows systems run: 
set PATH=%NDDSHOME%\lib\i86Win32jdk;%PATH%

On Unix systems except MacOS X (assuming you are using Bash) run:
export LD_LIBRARY_PATH=$NDDSHOME/lib/<platform_name>jdk:$LD_LIBRARY_PATH

On MacOSX (assuming your are using Bash) run:
export DYLD_LIBRARY_PATH=$NDDSHOME/lib/<platform_name>jdk:$DYLD_LIBRARY_PATH

Then, in two separate command prompt windows for the publisher and subscriber. 
Run the following commands from the example directory (this is necessary to 
ensure the application loads the QoS defined in USER_QOS_PROFILES.xml):

On Windows systems run:

java -cp .;%NDDSHOME%\class\nddsjava.jar cftPublisher  <domain_id> <samples_to_send>
java -cp .;%NDDSHOME%\class\nddsjava.jar cftSubscriber <domain_id> <sleep_periods> <select_cft>

On Unix systems (including Linux and MacOS X) run:

java -cp .:$NDDSHOME/class/nddsjava.jar cftPublisher  <domain_id> <samples_to_send>
java -cp .:$NDDSHOME/class/nddsjava.jar cftSubscriber <domain_id> <sleep_periods> <select_cft>


The applications accept two arguments:

   1. The <domain_id>. Both applications must use the same domain ID in order to 
   communicate. The default is 0.
   2. How long the examples should run, measured in samples for the publisher 
   and sleep periods for the subscriber. A value of '0' instructs the 
   application to run forever; this is the default.
   3. (subscriber only) The "select content filtered topic" switch. If 1, then 
   we use a content filtered topic. If 0, then we use a normal topic. The 
   default is 1.
