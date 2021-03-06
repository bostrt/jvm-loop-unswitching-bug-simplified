## What is this?

All credit for this particular reproducer goes to [rholder](https://github.com/rholder). This repository just contains a stupid simple version of his reproducer that only needs `java` and `javac`.

## How to use

If you are *trying* to reproduce the issue then make sure you have an old Java version. Below, you can see I'm using 1.7.0_55 which is older than the verion where the bug was fixed (in 1.7.0_60+ or 1.8+).

```
# java -version
java version "1.7.0_55"
OpenJDK Runtime Environment (rhel-2.4.7.2.el7_0-x86_64 u55-b13)
OpenJDK 64-Bit Server VM (build 24.51-b03, mixed mode)

# javac -cp ./httpclient-4.2.2.jar:./commons-lang-2.6.jar:./httpcore-4.2.2.jar JvmBug.java
# java -cp .:./httpclient-4.2.2.jar:./commons-lang-2.6.jar:./httpcore-4.2.2.jar JvmBug
```

Eventually, the second command that runs the reproducer should result in someting like:

```
# A fatal error has been detected by the Java Runtime Environment:
#
#  SIGSEGV (0xb) at pc=0x00007fc3f90751a1, pid=75921, tid=140479307597568
#
# JRE version: OpenJDK Runtime Environment (7.0_55-b13) (build 1.7.0_55-mockbuild_2014_05_30_13_47-b00)
# Java VM: OpenJDK 64-Bit Server VM (24.51-b03 mixed mode linux-amd64 compressed oops)
# Problematic frame:
# J  org.apache.http.impl.cookie.BestMatchSpec.formatCookies(Ljava/util/List;)Ljava/util/List;
#
# Failed to write core dump. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again
#
# An error report file with more information is saved as:
```
