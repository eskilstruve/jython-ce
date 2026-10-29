# Jython-ce: Python for the Java Platform (Community Edition)

Jython-ce (Jython community edition) is a community-maintained fork of
[Jython](https://github.com/jython/jython),
the implementation of Python in Java.
It tracks upstream Jython 2.7 and aims to keep it running well
on current releases of Java.
Only version 2.7 of Python can be supported at present.

Jython-ce remains compatible with upstream Jython:
the Java packages are still `org.python.*`,
the launcher is still `jython`,
and `platform.python_implementation()` still reports `'Jython'`,
so existing applications and libraries work unchanged.

## Compatibility

Jython provides good compatibility with Python 2.7 *the language*.
Also, a high proportion of the standard library is included,
taken from late versions of CPython (around 2.7.13).
Some standard library modules have a Jython-specific implementation
that has not kept pace with its CPython counterpart.

Jython 2.7 support for the Python ecosystem
includes built-in support of *pip/setuptools*.
You can use `bin/pip` if the targets do not include `C` extensions.
There is a native launcher for Windows (`bin/jython.exe`)
that works essentially like the `python` command.

Jim Baker presented a talk at PyCon 2015 about Jython 2.7,
including demos of new features: https://www.youtube.com/watch?v=hLm3garVQFo

## Support

Python 2.7 (the language) is no longer supported by the PSF.
Running on Jython should not be considered an alternative to porting your
application to Python 3, due to the limitations cited here
and the small amount of effort available to support 2.7.x.
Jython 2.7 is offered for continuity because a 3.x is not yet available.

See [ACKNOWLEDGMENTS](ACKNOWLEDGMENTS) for details about Jython's copyright,
license, contributors, and mailing lists.
Consult [NEWS](NEWS) for detailed release notes, including bugs fixed,
backward breaking changes, and new features.
We sincerely thank all who contribute to Jython, by bug reports, patches,
pull requests, documentation changes and e-mail discussions.

## Downloads

Jython-ce releases are published on the
[GitHub releases page](https://github.com/eskilstruve/jython-ce/releases).
Maven and Gradle artifacts use the group ID `io.github.eskilstruve`
(upstream Jython uses `org.python`).

## How to build Jython-ce

The project uses Git for version-control,
and the repository is at https://github.com/eskilstruve/jython-ce.
You should clone this repository to create a buildable copy of the latest state
of the Jython-ce source:
```
git clone https://github.com/eskilstruve/jython-ce.git
```
Start a new branch for any bug-fix or experimentation you plan.

Upstream Jython is developed at https://github.com/jython/jython.

### Build using `ant` for development

Jython-ce is normally built using `ant`.
It is necessary to have Ant and at least a Java 8 SDK on the path.
Jython-ce supports Java 8 through Java 26.
To build Jython in development, we generally use the command:
```
ant
```
This leaves an executable in `dist/bin`
that you may run from the check-out root with:
```
dist/bin/jython
```
Other `ant` targets exist, notably `clean`, `javatest` and `jar`.

You can test your build of Jython (by running the regression tests),
with the command:
```
dist/bin/jython -m test.regrtest -e -m regrtest_memo.txt
```
or by invoking the Ant target `regrtest`.

### Build an installer using `ant`

If you want to install a snapshot build of Jython-ce, use the command:
```
ant installer
```
This will leave you with a snapshot installer JAR in `dist`,
that you can run with:
```
java -jar jython-installer.jar
```
for the graphical installer, or:
```
java -jar jython-installer.jar --console
```
For the console version. (A `--help` option gives you the full story.)

### Build a JAR using Gradle

We have a Gradle build that results in a family of JARs and a POM.
It uses Gradle 9 (through the wrapper), which needs Java 17 or later to run,
although the JARs it produces still run on Java 8.
This is intended to provide the Jython-ce core in a form that Gradle and Maven
users can consume as a dependency.
Invoke this with:
```
PS> .\gradlew publish
```
and a JAR and POM are delivered to `build2\stagingRepo`.

Whereas the JARs delivered by the installer are somewhat "fat",
embedding certain dependencies in shaded (renamed) form,
the JAR from the Gradle build is "spare"
and cites its dependencies externally through a POM.

## Other Useful Documentation

[Project Processes](ProcessDocs)

