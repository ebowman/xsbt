[Google Code]: http://code.google.com/p/simple-build-tool
[Northeast Scala Symposium]: http://www.nescala.org/2011/
[Scala Days 2011]: http://days2011.scala-lang.org/node/138/285
[documentation]: http://www.scala-sbt.org/release/docs/
[Setup]: http://www.scala-sbt.org/release/docs/Getting-Started/Setup
[video of a demo]: http://vimeo.com/20263617
[FAQ]: http://www.scala-sbt.org/release/docs/faq

# sbt 0.13

This is the 0.13.x series of sbt.

 * [Setup]: Describes getting started with the latest binary release.  See below to build from source.
 * [FAQ]: Explains how to get help, how to report an issue, and how to contribute.
 * There is a [video of a demo] given at [Scala Days 2011] based on sbt 0.10.0 that gives an introduction to the configuration system in sbt 0.10.0 and later.  See the [documentation] for current information.
 * [Google Code]: hosts sbt 0.7.7 and earlier versions

# Build from source

1. Install the current stable binary release of sbt (see [Setup]), which will be used to build sbt from source.
2. Get the source code.

		$ git clone git://github.com/harrah/xsbt.git
		$ cd xsbt

3. The initial branch is the development branch 0.13, which contains the latest code for the next major sbt release.  To build a specific release or commit, switch to the associated tag.  The tag for the latest stable release is v0.12.1:

		$ git checkout v0.12.1

	Note that sbt is always built with the previous stable release.  For example, the 0.13 branch is built with 0.12.1, the v0.11.2 tag is built with 0.11.1, and the v0.11.0 tag is built with 0.10.1.

4. To build the launcher, publish all components locally, and build API and SXR documentation:

		$ sbt build-all

	Alternatively, the individual commands run by `build-all` may be executed directly:

		$ sbt publish-local proguard sxr doc

5. To use this locally built version of sbt, copy your stable `~/bin/sbt` script to `~/bin/xsbt` and change it to use the launcher jar in `<xsbt>/target/`.  For the v0.12.1 tag, the full location is:

		<xsbt>/target/sbt-launch-0.12.1.jar

	If using the 0.13 development branch, the launcher is at:

		<xsbt>/target/sbt-launch-0.13.0-SNAPSHOT.jar

## Modifying sbt

1. New development takes place on the 0.13 branch.  Fixes and improvements that are binary compatible with 0.12 can be backported to the 0.12 branch at the time of the next release.

2. When developing sbt itself, there is no need to run `build-all`, since this generates documentation as well.  For the fastest turnaround time for checking compilation only, run `compile`.

3. To use your modified version of sbt in a project locally, run `publish-local`.  If you have modified the launcher, also run `proguard`.

4. After each `publish-local`, clean the `~/.sbt/boot/` directory.  Alternatively, if sbt is running and the launcher hasn't changed, run `reboot full` to have sbt do this for you.

5. If a project has `project/build.properties` defined, either delete the file or change `sbt.version` to `0.13.0-SNAPSHOT`.

## Building Documentation

Documentation is built using sphinx and requires some external programs and libraries to be manually installed first:

```text
$ pip install pygments
$ pip install sphinx
$ pip install sphinxcontrib-issuetracker
```

To build the full site, run the `make-site` task, which will generate the manual, API, SXR, and other site pages in `target/site/`.
To only work on the site and not API or SXR, run `sphinx:mappings`.