Errorified: a simple exception formatter in Scala
=================================================

What does it do?
----------------

It takes a Java Throwable, and:

- navigates all nested exceptions, including for exceptions which don't support Java 1.4's `getCause()`
- finds application-specific location information
- neatly combines the common sections of nested stack traces
- can remove stack entries in the middle of a trace when a maximum of entries is reached
- formats everything into something you can output in your log file

How do I use it?
----------------

Create an object extending `Formatter` with some configuration:

    import org.orbeon.errorified._

    object MyFormatter extends Formatter {
        val Width = 120
        val MaxStackLength = 40
    }

You then use it as follows:

    MyFormatter.format(myThrowable)

You can optionally override two methods to refine how the main error message is obtained as well as providing
application-specific location information:

    import org.orbeon.errorified._

    object MyFormatter extends Formatter {
        val Width = 120
        val MaxStackLength = 40

        override def getThrowableMessage(throwable: Throwable) = ...
        override def getAllLocationData(t: Throwable) = ...
    }

How do I build it?
------------------

    mvn install

Other things I need to know?
----------------------------

- it's written in Scala (tested with 2.9.2)
- it's released under the MIT license

---

Copyright 2012 (C) Orbeon, Inc.
