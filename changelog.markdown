
[comment]: # (Before releasing, make sure to follow the steps in https://github.com/nim-lang/nimble/wiki/Releasing-a-new-version)

# Nimble changelog

## 0.8.4 - 29/01/2017

Another bug fix release which resolves problems related to stale nimscriptapi
files in /tmp/, no compilation output when ``nimble build`` fails, and issues
with the new package validation on Windows.

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.8.2...v0.8.4

## 0.8.2 - 08/01/2017

This is a small bug fix release which resolves problems with the installation
of Aporia (and likely other Nimble packages).

## 0.8.0 - 05/01/2017

This is a large release containing multiple new features and many bug fixes.

* Implemented a completely new output system.
  * Supports different message types and priorities. Each is differently
    encoded using a color and a brightness.
  * The amount of messages shown can be changed by using the new ``--verbose``
    and ``--debug`` flags, by default only high priority messages are shown.
  * Duplicate warnings are filtered out to prevent too much noise.
* Package namespaces are now validated. You will see a warning whenever an
  incorrectly namespaced package is read by Nimble, this can occur either
  during installation or when the installed package database is being loaded.
  The namespacing rules are described in Nimble's
  [readme](https://github.com/nim-lang/nimble#libraries).
  **Consider these warnings to be unstable, if you see something that you
  think is incorrect please report it**.
* Special version dependencies are now installed into a directory with that
  special version in its name. For example, ``compiler@#head`` will be installed
  into ``~/.nimble/pkgs/compiler-#head``. This reduces the amount of redundant
  installs. See [#88](https://github.com/nim-lang/nimble/issues/88) for
  more information.
* External dependencies can now be specified in .nimble files. Nimble doesn't
  install these, but does instruct the user on how they can be installed.
  More information about this feature can be found in the
  [readme](https://github.com/nim-lang/nimble#external-dependencies).
* Nimble now supports package aliases in the packages.json files.
* Fixed regression that caused transitive dependencies to not be installed.
* Fixed problem with ``install`` command when a ``src`` directory is present
  in the current directory.
* Improved quoting of process execution arguments.
* Many improvements to custom ``--nimbleDir`` handling. All commands should now
  support it correctly.
* Running ``nimble -v`` will no longer read the Nimble config before displaying
  the version.
* Refresh command now supports a package list name as argument.
* Fixes issues with symlinks not being removed correctly.
* Changed the way the ``dump`` command locates the .nimble file.

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.7.10...v0.8.0

Full list of issues which have been closed: https://github.com/nim-lang/nimble/issues?utf8=%E2%9C%93&q=is%3Aissue+closed%3A%222016-10-09+..+2017-01-05%22+

## 0.7.10 - 09/10/2016

This release includes multiple bug fixes.

* Reverted patch that breaks binary stubs in Git Bash on Windows.
* The ``nimscriptapi.nim`` file is now statically compiled into the binary.
  This should fix the "could not find nimscriptapi.nim" errors. The file can
  still be overriden by placing a file named ``nimscriptapi.nim`` inside a
  ``nimblepkg`` directory that is placed alongside the Nimble binary, or
  by a ``nimscriptapi.nim`` file inside ``~/.nimble/pkgs/nimble-ver/nimblepkg/``.
  For more information see the
  [code that looks for this file](https://github.com/nim-lang/nimble/blob/v0.7.10/src/nimblepkg/nimscriptsupport.nim#L176).
* Nim files can now be imported in .nimble nimscript files. (Issue [#186](https://github.com/nim-lang/nimble/issues/186))
* Requiring a specific git commit hash no longer fails. (Issue [#129](https://github.com/nim-lang/nimble/issues/129))

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.7.8...v0.7.10

## 0.7.8 - 28/09/2016

This is a hotfix release which fixes crashes when Nimble (or Nim) is installed
to ``C:\Program Files`` or other paths with spaces in them.

## 0.7.6 - 26/09/2016

This is a small release designed to coincide with the release of Nim 0.15.0.

* Fixes ``--depsOnly`` flag ([commit](https://github.com/nim-lang/nimble/commit/f6a19b54e47c7c99f2b473fc02915277273f8c41))
* Fixes compilation on 0.15.0.
* Fixes #239.
* Fixes #215.
* VCS information is now stored in the Nimble package metadata.

## 0.7.4 - 06/06/2016

This release is mainly a bug fix release. The installation problems
introduced by v0.7.0 should now be fixed.

* Fixed symlink install issue
  (Thank you [@yglukhov](https://github.com/yglukhov)).
* Fixed permission issue when installing packages
  (Thank you [@SSPkrolik](https://github.com/SSPkrolik)).
* Work around for issue #204.
  (Thank you [@Jeff-Ciesielski](https://github.com/Jeff-Ciesielski)).
* Fixed FD leak.
  (Thank you [@yglukhov](https://github.com/yglukhov)).
* Implemented the ``--depsOnly`` option for the ``install`` command.
* Various fixes to installation/nimscript support problems introduced by
v0.7.0.

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.7.2...v0.7.4

## 0.7.2 - 11/02/2016

This is a hotfix release which alleviates problems when building Nimble.

See Issue [#203](https://github.com/nim-lang/nimble/issues/203) for more
information.

## 0.7.0 - 30/12/2015

This is a major release.
Significant changes include NimScript support, configurable package list
URLs, a new ``publish`` command, the removal of the dependency on
OpenSSL, and proxy support. More detailed list of changes follows:

* Fixed ``chcp`` on Windows XP and Windows Vista
  (Thank you [@vegansk](https://github.com/vegansk)).
* Fixed incorrect command line processing
  (Issue [#151](https://github.com/nim-lang/nimble/issues/151))
* Merged ``developers.markdown`` back into ``readme.markdown``
  (Issue [#132](https://github.com/nim-lang/nimble/issues/132))
* Removed advertising clause from license
  (Issue [#153](https://github.com/nim-lang/nimble/issues/153))
* Implemented ``publish`` command
  (Thank you for taking the initiative [@Araq](https://github.com/Araq))
* Implemented NimScript support. Nimble now import a portion of the Nim
  compiler source code for this.
  (Thank you for taking the initiative [@Araq](https://github.com/Araq))
* Fixes incorrect logic for finding the Nim executable
  (Issue [#125](https://github.com/nim-lang/nimble/issues/125)).
* Renamed the ``update`` command to ``refresh``. **The ``update`` command will
  mean something else soon!**
  (Issue [#158](https://github.com/nim-lang/nimble/issues/158))
* Improvements to the ``init`` command.
  (Issue [#96](https://github.com/nim-lang/nimble/issues/96))
* Package names must now officially be valid Nim identifiers. Package's
  with dashes in particular will become invalid in the next version.
  Warnings are shown now but the **next version will show an error**.
  (Issue [#126](https://github.com/nim-lang/nimble/issues/126))
* Added error message when no build targets are present.
  (Issue [#108](https://github.com/nim-lang/nimble/issues/108))
* Implemented configurable package lists. Including fallback URLs
  (Issue [#75](https://github.com/nim-lang/nimble/issues/75)).
* Removed the OpenSSL dependency
  (Commit [ec96ee7](https://github.com/nim-lang/nimble/commit/ec96ee7709f0f8bd323aa1ac5ed4c491c4bf23be))
* Implemented proxy support. This can be configured using the ``http_proxy``/
  ``https_proxy`` environment variables or Nimble's configuration
  (Issue [#86](https://github.com/nim-lang/nimble/issues/86)).
* Fixed issues with reverse dependency storage
  (Issue [#113](https://github.com/nim-lang/nimble/issues/113) and
   [#168](https://github.com/nim-lang/nimble/issues/168)).

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.6.2...v0.7.0

## 0.6.4 - 30/12/2015

This is a hotfix release fixing compilation with Nim 0.12.0.

See Issue [#180](https://github.com/nim-lang/nimble/issues/180) for more
info.

## 0.6.2 - 19/06/2015

* Added ``binDir`` option to specify where the build output should be placed
  (Thank you [@minciue](https://github.com/minciue)).
* Fixed deprecated code (Thank you [@lou15b](https://github.com/lou15b)).
* Fixes to old ``.babel`` folder handling
  (Thank you [@ClementJnc](https://github.com/ClementJnc)).
* Added ability to list only the installed packages via
  ``nimble list --installed`` (Thank you
  [@hiteshjasani](https://github.com/hiteshjasani).
* Fixes compilation with Nim v0.11.2 (Thank you
  [@JCavallo](https://github.com/JCavallo)).
* Implements the ``--nimbleDir`` option (Thank you
  [@ClementJnc](https://github.com/ClementJnc)).
* [Fixes](https://github.com/nim-lang/nimble/issues/128) ``nimble uninstall``
  not giving an error when no package name is
  specified (Thank you [@dom96](https://github.com/dom96)).
* [When](https://github.com/nim-lang/nimble/issues/139) installing and building
  a tagged version of a package fails, Nimble will
  now attempt to install and build the ``#head`` of the repo
  (Thank you [@dom96](https://github.com/dom96)).
* [Fixed](https://github.com/nim-lang/nimble/commit/1234cdce13c1f1b25da7980099cffd7f39b54326)
  cloning of git repositories with non-standard default branches
  (Thank you [@dom96](https://github.com/dom96)).

----

Full changelog: https://github.com/nim-lang/nimble/compare/v0.6...v0.6.2

## 0.6.0 - 26/12/2014

* Renamed from Babel to Nimble
* Introduces compatibility with Nim v0.10.0+
* Implemented the ``init`` command which generates a .nimble file for new
  projects. (Thank you
  [@singularperturbation](https://github.com/singularperturbation))
* Improved cloning of git repositories.
  (Thank you [@gradha](https://github.com/gradha))
* Fixes ``path`` command issues (Thank you [@gradha](https://github.com/gradha))
* Fixes problems with symlinking when there is a space in the path.
  (Thank you [@philip-wernersbach](https://github.com/philip-wernersbach))
* The code page will now be changed when executing Nimble binary packages.
  This adds support for Unicode in cmd.exe (#54).
* ``.cmd`` files are now used in place of ``.bat`` files. Shell files for
  Cygwin/Git bash are also now created.

## 0.4.0 - 24/06/2014

* Introduced the ability to delete packages.
* When installing packages, a list of files which have been copied is stored
  in the babelmeta.json file.
* When overwriting an already installed package babel will no longer delete
  the whole directory but only the files which it installed.
* Versions are now specified on the command line after the '@' character when
  installing and uninstalling packages. For example: ``babel install foobar@0.1``
  and ``babel install foobar@#head``.
* The babel package installation directory can now be changed in the new
  config.
* Fixes a number of issues.
