/*
 * Copyright 2013-14 Fraunhofer ISE
 *
 * This file is part of j62056.
 * For more information visit http://www.openmuc.org
 *
 * j62056 is free software: you can redistribute it and/or modify
 * it under the terms of the GNU Lesser General Public License as published by
 * the Free Software Foundation, either version 2.1 of the License, or
 * (at your option) any later version.
 *
 * j62056 is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU Lesser General Public License for more details.
 *
 * You should have received a copy of the GNU Lesser General Public License
 * along with j62056.  If not, see <http://www.gnu.org/licenses/>.
 *
 */

Author: Stefan Feuerhahn

j62056 is a Java library implementing an IEC 62056-21 mode C
master.  It can be used to read metering data from slaves such as gas,
water, heat, or electricity meters.

The message exchange follows a very simple procedure in this protocol:
Master --------Request message (300 baud)--------> Slave
Master <----Identification message (300 baud)----- Slave
Master --------Acknowledgment (300 baud)---------> Slave
Master <---------Data message (new baud rate)----- Slave

-The library and its dependencies are found in the folders
 "build/libs/" and "dependencies"
-Javadocs can be found in the build/javadoc folder

For the latest release of this software visit http://www.openmuc.org .


Read Meter Application:
-----------------------
The library includes an application that reads a given meter and
prints the received data sets to stdout. This application can also be
used as an example on how to use the the library. You can find the
source code of ReadMeter.java in src/main/java/org/openmuc/j62056/.

You can can execute ReadMeter from the console with the following
command (from this projects root directory):
Linux/Unix:
>java -cp "build/libs/j62056-<version>.jar:dependencies/rxtxcomm_api-2.2pre2-11_bundle.jar" org.openmuc.j62056.ReadMeter
Windows:
>java -cp "build\libs\j62056-<version>.jar;dependencies\rxtxcomm_api-2.2pre2-11_bundle.jar" org.openmuc.j62056.ReadMeter

Sometimes you might have to add a system property so that java finds
the jni libs. e.g.: -Djava.library.path=/usr/lib/jni

As an alternative you can create Eclipse project files as explained here:
http://www.openmuc.org/index.php?id=28 and run ReadMeter from within
Eclipse


RXTX - Java library for serial communication
--------------------------------------------

Note that j62056 depends on the Java library RXTX
(http://rxtx.qbang.org). A binary version of this library can be found
in the dependencies folder. This library in turn depends on native
libraries that you have to install first. Many Linux distributions
offer the package librxtx-java to install these native libraries. For
instructions on how to install these on Windows visit
http://rxtx.qbang.org/wiki/index.php/Installation_for_Windows

RXTX (Copyright 1997-2004 by Trent Jarvi) is licensed under LGPL(v2 or
later). Beware there exist several different versions of
rxtxcomm-2.2pre2. The version of RXTX in the depencies folder was
taken from Debian (version 2.2pre2-11) and has many bug fixes compared
to the latest version on the website. This version was converted to a
bundle using bnd: "java -jar bnd/bnd-1.50.0.jar wrap
RXTXcomm-2.2pre2.jar". The source code of this version can be obtained
from the Debian rxtx src package. E.g. from here:
http://packages.ubuntu.com/source/saucy/rxtx


Develop j62056:
---------------

We use the Gradle build automation tool. The distribution contains a
fully functional gradle build file ("build.gradle"). Thus if you
changed code and want to rebuild a library you can do it easily with
Gradle. Also if you want to import our software into Eclipse you can
easily create Eclipse project files using Gradle. Just follow these
instructions (for the most up to date version of these instructions
visit http://www.openmuc.org/index.php?id=28):

Install Gradle: 

- Download Gradle from the website: www.gradle.org

- Set the PATH variable: e.g. in Linux add to your .bashrc: export
  PATH=$PATH:/home/user/path/to/gradle-version/bin

- If you're behind a proxy you can set the proxy options in the
  gradle.properties file as explained here:
  http://www.gradle.org/docs/current/userguide/build_environment.html.

- Setting "org.gradle.daemon=true" in gradle.properties will speed up
  Gradle

Create Eclipse project files using Gradle:

- with the command "gradle eclipse" you can generate Eclipse project
  files

- It is important to add the GRADLE_USER_HOME variable in Eclipse:
  Window->Preferences->Java->Build Path->Classpath Variable. Set it to
  the path of the .gradle folder in your home directory
  (e.g. /home/someuser/.gradle (Unix) or C:/Documents and
  Settings/someuser/.gradle (Windows))

Rebuild a library:

- After you have modified the code you can completely rebuild the code
  using the command "gradle clean build" This will also execute the
  junit tests.

- You can also assemble a new distribution tar file: the command
  "gradle clean tar" will build everything and put a new distribution
  file in the folder "build/distribution".

