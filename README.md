jruby-cext: CRuby extension support for JRuby
=============================================

This library provides a CRuby compatible C extension API for JRuby, via Java's
JNI subsystem.

Building
--------

Ant is required, since there's Java portions of the C ext support. "ant" will
build the Java and C pieces and put the artifacts in the "build" directory.

Status
------

C extension support was deprecated as part of JRuby propert in the 1.7.x line,
and will be removed in a future release. This project represents that support
pulled out to a separate repository, so that users can help maintain it
independently of JRuby core.

Currently, support is only partial and only for 1.8 C API features. We are
missing many APIs for 1.8 support and most 1.9-specific APIs.

Limitations
-----------

Loading a C extension into JRuby requires that there be only one JRuby
instance in a given JVM using C extensions. This is because there's no way
in the CRuby API to identify which JRuby instance a given extension is
associated with.

All call-outs to C extensions from JRuby are synchronized against a single
lock, to avoid concurrency issues at the C level. This may be something we
can remove, since Rubinius has done so to improve concurrency in C extensions
and so far that has worked out.

Calls from C to Ruby or Ruby to C have more overhead than in C Ruby, mostly
due to the necessity of proxying everything through JNI, providing virtual
handle objects instead of direct pointers, and copying or marshaling Array
and String data back and forth as it is modified.

Contributing
------------

The JRuby core team does not have resources or expertise to maintain this C
extension support, so we have spun it off from JRuby core in hopes that the
Ruby/JRuby community can help us improve and maintain it. If you are
interested in helping, we will provide support from the JRuby/JVM side and
give you access to commit freely to the repository.
