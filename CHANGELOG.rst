1.11.0+sp1 (2024-05-20)
===================

- fix CVE-2022-42969

1.11.0 (2021-11-04)
===================

- Support Python 3.11
- Support ``NO_COLOR`` environment variable
- Update vendored apipkg: 1.5 => 2.0

1.10.0 (2020-12-12)
===================

- Fix a regular expression DoS vulnerability in the py.path.svnwc SVN blame functionality (CVE-2020-29651)
- Update vendored apipkg: 1.4 => 1.5
- Update vendored iniconfig: 1.0.0 => 1.1.1

1.9.0 (2020-06-24)
==================

- Add type annotation stubs for the following modules:

  * ``py.error``
  * ``py.iniconfig``
  * ``py.path`` (not including SVN paths)
  * ``py.io``
  * ``py.xml``

  There are no plans to type other modules at this time.

  The type annotations are provided in external .pyi files, not inline in the
  code, and may therefore contain small errors or omissions. If you use ``py``
  in conjunction with a type checker, and encounter any type errors you believe
  should be accepted, please report it in an issue.

1.8.2 (2020-06-15)
==================

- On Windows, ``py.path.local``s which differ only in case now have the same
  Python hash value. Previously, such paths were considered equal but had
  different hashes, which is not allowed and breaks the assumptions made by
  dicts, sets and other users of hashes.

1.8.1 (2019-12-27)
==================

- Handle ``FileNotFoundError`` when trying to import pathlib in ``path.common``
  on Python 3.4 (#207).

- ``py.path.local.samefile`` now works correctly in Python 3 on Windows when dealing with symlinks.

1.8.0 (2019-02-21)
==================

- add ``"importlib"`` pyimport mode for python3.5+, allowing unimportable test suites
  to contain identically named modules.

- fix ``LocalPath.as_cwd()`` not calling ``os.chdir()`` with ``None``, when
  being invoked from a non-existing directory.


1.7.0 (2018-10-11)
==================

- fix #174: use ``shutil.get_terminal_size()`` in Python 3.3+ to determine the size of the
  terminal, which produces more accurate results than the previous method.

- fix pytest-dev/pytest#2042: introduce new ``PY_IGNORE_IMPORTMISMATCH`` environment variable
  that suppresses ``ImportMismatchError`` exceptions when set to ``1``.


1.6.0 (2018-08-27)
==================

- add ``TerminalWriter.width_of_current_line`` (i18n version of
  ``TerminalWriter.chars_on_current_line``), a read-only property
  that tracks how wide the current line is, attempting to take
  into account international characters in the calculation.

1.5.4 (2018-06-27)
==================

- fix pytest-dev/pytest#3451: don't make assumptions about fs case sensitivity
  in ``make_numbered_dir``.

1.5.3
=====

- fix #179: ensure we can support 'from py.error import ...'

1.5.2
=====

- fix #169, #170: error importing py.log on Windows: no module named ``syslog``.

1.5.1
=====

- fix #167 - prevent pip from installing py in unsupported Python versions.

1.5.0
=====

NOTE: **this release has been removed from PyPI** due to missing package
metadata which caused a number of problems to py26 and py33 users.
This issue was fixed in the 1.5.1 release.

- python 2.6 and 3.3 are no longer supported
- deprecate py.std and remove all internal uses
- fix #73 turn py.error into an actual module
- path join to / no longer produces leading double slashes
- fix #82 - remove unsupportable aliases
- fix python37 compatibility of path.sysfind on windows by correctly replacing vars
- turn iniconfig and apipkg into vendored packages and ease de-vendoring for distributions
- fix #68 remove invalid py.test.ensuretemp references
- fix #25 - deprecate path.listdir(sort=callable)
- add ``TerminalWriter.chars_on_current_line`` read-only property that tracks how many characters
  have been written to the current line.

1.4.34
====================================================================

- fix issue119 / pytest issue708 where tmpdir may fail to make numbered directories
  when the filesystem is case-insensitive.

1.4.33
====================================================================

- avoid imports in calls to py.path.local().fnmatch(). Thanks Andreas Pelme for
  the PR.

- fix issue106: Naive unicode encoding when calling fspath() in python2. Thanks Tiago Nobrega for the PR.

- fix issue110: unittest.TestCase.assertWarns fails with py imported.

1.4.32
====================================================================

- fix issue70: added ability to copy all stat info in py.path.local.copy.

- make TerminalWriter.fullwidth a property.  This results in the correct
  value when the terminal gets resized.

- update supported html tags to include recent additions.
  Thanks Denis Afonso for the PR.

- Remove internal code in ``Source.compile`` meant to support earlier Python 3 versions that produced the side effect
  of leaving ``None`` in ``sys.modules`` when called (see pytest-dev/pytest#2103).
  Thanks Bruno Oliveira for the PR.

1.4.31
==================================================

- fix local().copy(dest, mode=True) to also work
  with unicode.

- pass better error message with svn EEXIST paths

1.4.30
==================================================

- fix issue68 an assert with a  multiline list comprehension
  was not reported correctly. Thanks Henrik Heibuerger.


1.4.29
==================================================

- fix issue55: revert a change to the statement finding algorithm
  which is used by pytest for generating tracebacks.
  Thanks Daniel Hahler for initial analysis.

- fix pytest issue254 for when traceback rendering can't
  find valid source code.  Thanks Ionel Cristian Maries.


1.4.28
==================================================

- fix issue64 -- dirpath regression when "abs=True" is passed.
  Thanks Gilles Dartiguelongue.

1.4.27
==================================================

- fix issue59: point to new repo site

- allow a new ensuresyspath="append" mode for py.path.local.pyimport()
  so that a neccessary import path is appended instead of prepended to
  sys.path

- strike undocumented, untested argument to py.path.local.pypkgpath

- speed up py.path.local.dirpath by a factor of 10

1.4.26
==================================================

- avoid calling normpath twice in py.path.local

- py.builtin._reraise properly reraises under Python3 now.

- fix issue53 - remove module index, thanks jenisys.

- allow posix path separators when "fnmatch" is called.
  Thanks Christian Long for the complete PR.

1.4.25
==================================================

- fix issue52: vaguely fix py25 compat of py.path.local (it's not
  officially supported), also fix docs

- fix pytest issue 589: when checking if we have a recursion error
  check for the specific "maximum recursion depth" text of the exception.

1.4.24
==================================================

- Fix retrieving source when an else: line has an other statement on
  the same line.

- add localpath read_text/write_text/read_bytes/write_bytes methods
  as shortcuts and clearer bytes/text interfaces for read/write.
  Adapted from a PR from Paul Moore.


1.4.23
==================================================

- use newer apipkg version which makes attribute access on
  alias modules resolve to None rather than an ImportError.
  This helps with code that uses inspect.getframeinfo()
  on py34 which causes a complete walk on sys.modules
  thus triggering the alias module to resolve and blowing
  up with ImportError.  The negative side is that something
  like "py.test.X" will now result in None instead of "importerror: pytest"
  if pytest is not installed.  But you shouldn't import "py.test"
  anyway anymore.

- adapt one svn test to only check for any exception instead
  of specific ones because different svn versions cause different
  errors and we don't care.


1.4.22
==================================================

- refactor class-level registry on ForkedFunc child start/finish
  event to become instance based (i.e. passed into the constructor)

1.4.21
==================================================

- ForkedFunc now has class-level register_on_start/on_exit()
  methods to allow adding information in the boxed process.
  Thanks Marc Schlaich.

- ForkedFunc in the child opens in "auto-flush" mode for
  stdout/stderr so that when a subprocess dies you can see
  its output even if it didn't flush itself.

- refactor traceback generation in light of pytest issue 364
  (shortening tracebacks).   you can now set a new traceback style
  on a per-entry basis such that a caller can force entries to be
  isplayed as short or long entries.

- win32: py.path.local.sysfind(name) will preferrably return files with
  extensions so that if "X" and "X.bat" or "X.exe" is on the PATH,
  one of the latter two will be returned.

1.4.20
==================================================

- ignore unicode decode errors in xmlescape.  Thanks Anatoly Bubenkoff.

- on python2 modify traceback.format_exception_only to match python3
  behaviour, namely trying to print unicode for Exception instances

- use a safer way for serializing exception reports (helps to fix
  pytest issue413)

Changes between 1.4.18 and 1.4.19
==================================================

- merge in apipkg fixes

- some micro-optimizations in py/_code/code.py for speeding
  up pytest runs.  Thanks Alex Gaynor for initiative.

- check PY_COLORS=1 or PY_COLORS=0 to force coloring/not-coloring
  for py.io.TerminalWriter() independently from capabilities
  of the output file.  Thanks Marc Abramowitz for the PR.

- some fixes to unicode handling in assertion handling.
  Thanks for the PR to Floris Bruynooghe.  (This helps
  to fix pytest issue 319).

- depend on setuptools presence, remove distribute_setup

Changes between 1.4.17 and 1.4.18
==================================================

- introduce path.ensure_dir() as a synonym for ensure(..., dir=1)

- some unicode/python3 related fixes wrt to path manipulations
  (if you start passing unicode particular in py2 you might
  still get problems, though)

Changes between 1.4.16 and 1.4.17
==================================================

- make py.io.TerminalWriter() prefer colorama if it is available
  and avoid empty lines when separator-lines are printed by
  being defensive and reducing the working terminalwidth by 1

- introduce optional "expanduser" argument to py.path.local
  to that local("~", expanduser=True) gives the home
  directory of "user".

Changes between 1.4.15 and 1.4.16
==================================================

- fix issue35 - define __gt__ ordering between a local path
  and strings

- fix issue36 - make chdir() work even if os.getcwd() fails.

- add path.exists/isdir/isfile/islink shortcuts

- introduce local path.as_cwd() context manager.

- introduce p.write(ensure=1) and p.open(ensure=1)
  where ensure triggers creation of neccessary parent
  dirs.


Changes between 1.4.14 and 1.4.15
==================================================

- majorly speed up some common calling patterns with
  LocalPath.listdir()/join/check/stat functions considerably.

- fix an edge case with fnmatch where a glob style pattern appeared
  in an absolute path.

Changes between 1.4.13 and 1.4.14
==================================================

- fix dupfile to work with files that don't
  carry a mode. Thanks Jason R. Coombs.

Changes between 1.4.12 and 1.4.13
==================================================

- fix getting statementrange/compiling a file ending
  in a comment line without newline (on python2.5)
- for local paths you can pass "mode=True" to a copy()
  in order to copy permission bits (underlying mechanism
  is using shutil.copymode)
- add paths arguments to py.path.local.sysfind to restrict
  search to the diretories in the path.
- add isdir/isfile/islink to path.stat() objects allowing to perform
  multiple checks without calling out multiple times
- drop py.path.local.__new__ in favour of a simpler __init__
- iniconfig: allow "name:value" settings in config files, no space after
  "name" required
- fix issue 27 - NameError in unlikely untested case of saferepr


Changes between 1.4.11 and 1.4.12
==================================================

- fix python2.4 support - for pre-AST interpreters re-introduce
  old way to find statements in exceptions (closes pytest issue 209)
- add tox.ini to distribution
- fix issue23 - print *,** args information in tracebacks,
  thanks Manuel Jacob


Changes between 1.4.10 and 1.4.11
==================================================

- use _ast to determine statement ranges when printing tracebacks -
  avoiding multi-second delays on some large test modules
- fix an internal test to not use class-denoted pytest_funcarg__
- fix a doc link to bug tracker
- try to make terminal.write() printing more robust against
  unicodeencode/decode problems, amend according test
- introduce py.builtin.text and py.builtin.bytes
  to point to respective str/unicode (py2) and bytes/str (py3) types
- fix error handling on win32/py33 for ENODIR

Changes between 1.4.9 and 1.4.10
==================================================

- terminalwriter: default to encode to UTF8 if no encoding is defined
  on the output stream
- issue22: improve heuristic for finding the statementrange in exceptions

Changes between 1.4.8 and 1.4.9
==================================================

- fix bug of path.visit() which would not recognize glob-style patterns
  for the "rec" recursion argument
- changed iniconfig parsing to better conform, now the chars ";"
  and "#" only mark a comment at the stripped start of a line
- include recent apipkg-1.2
- change internal terminalwriter.line/reline logic to more nicely
  support file spinners

Changes between 1.4.7 and 1.4.8
==================================================

- fix issue 13 - correct handling of the tag name object in xmlgen
- fix issue 14 - support raw attribute values in xmlgen
- fix windows terminalwriter printing/re-line problem
- update distribute_setup.py to 0.6.27

Changes between 1.4.6 and 1.4.7
==================================================

- fix issue11 - own test failure with python3.3 / Thanks Benjamin Peterson
- help fix pytest issue 102

Changes between 1.4.5 and 1.4.6
==================================================

- help to fix pytest issue99: unify output of
  ExceptionInfo.getrepr(style="native") with ...(style="long")
- fix issue7: source.getstatementrange() now raises proper error
  if no valid statement can be found
- fix issue8: fix code and tests of svnurl/svnwc to work on subversion 1.7 -
  note that path.status(updates=1) will not properly work svn-17's status
  --xml output is broken.
- make source.getstatementrange() more resilent about non-python code frames
  (as seen from jnja2)
- make trackeback recursion detection more resilent
  about the eval magic of a decorator library
- iniconfig: add support for ; as comment starter
- properly handle lists in xmlgen on python3
- normalize py.code.getfslineno(obj) to always return a (string, int) tuple
  defaulting to ("", -1) respectively if no source code can be found for obj.

Changes between 1.4.4 and 1.4.5
==================================================

- improve some unicode handling in terminalwriter and capturing
  (used by pytest)

Changes between 1.4.3 and 1.4.4
==================================================

- a few fixes and assertion related refinements for pytest-2.1
- guard py.code.Code and getfslineno against bogus input
  and make py.code.Code objects for object instance
  by looking up their __call__ function.
- make exception presentation robust against invalid current cwd

Changes between 1.4.2 and 1.4.3
==================================================

- fix terminal coloring issue for skipped tests (thanks Amaury)
- fix issue4 - large calls to ansi_print (thanks Amaury)

Changes between 1.4.1 and 1.4.2
==================================================

- fix (pytest) issue23 - tmpdir argument now works on Python3.2 and WindowsXP
  (which apparently starts to offer os.symlink now)

- better error message for syntax errors from compiled code

- small fix to better deal with (un-)colored terminal output on windows

Changes between 1.4.0 and 1.4.1
==================================================

- fix issue1 - py.error.* classes to be pickleable

- fix issue2 - on windows32 use PATHEXT as the list of potential
  extensions to find find binaries with py.path.local.sysfind(commandname)

- fix (pytest-) issue10 and refine assertion reinterpretation
  to avoid breaking if the __nonzero__ of an object fails

- fix (pytest-) issue17 where python3 does not like "import *"
  leading to misrepresentation of import-errors in test modules

- fix py.error.* attribute pypy access issue

- allow path.samefile(arg) to succeed when arg is a relative filename

- fix (pytest-) issue20 path.samefile(relpath) works as expected now

- fix (pytest-) issue8 len(long_list) now shows the lenght of the list

Changes between 1.3.4 and 1.4.0
==================================================

- py.test was moved to a separate "pytest" package. What remains is
  a stub hook which will proxy ``import py.test`` to ``pytest``.
- all command line tools ("py.cleanup/lookup/countloc/..." moved
  to "pycmd" package)
- removed the old and deprecated "py.magic" namespace
- use apipkg-1.1 and make py.apipkg.initpkg|ApiModule available
- add py.iniconfig module for brain-dead easy ini-config file parsing
- introduce py.builtin.any()
- path objects have a .dirname attribute now (equivalent to
  os.path.dirname(path))
- path.visit() accepts breadthfirst (bf) and sort options
- remove deprecated py.compat namespace

Changes between 1.3.3 and 1.3.4
==================================================

- fix issue111: improve install documentation for windows
- fix issue119: fix custom collectability of __init__.py as a module
- fix issue116: --doctestmodules work with __init__.py files as well
- fix issue115: unify internal exception passthrough/catching/GeneratorExit
- fix issue118: new --tb=native for presenting cpython-standard exceptions

Changes between 1.3.2 and 1.3.3
==================================================

- fix issue113: assertion representation problem with triple-quoted strings
  (and possibly other cases)
- make conftest loading detect that a conftest file with the same
  content was already loaded, avoids surprises in nested directory structures
  which can be produced e.g. by Hudson. It probably removes the need to use
  --confcutdir in most cases.
- fix terminal coloring for win32
  (thanks Michael Foord for reporting)
- fix weirdness: make terminal width detection work on stdout instead of stdin
  (thanks Armin Ronacher for reporting)
- remove trailing whitespace in all py/text distribution files

Changes between 1.3.1 and 1.3.2
==================================================

New features
++++++++++++++++++

- fix issue103:  introduce py.test.raises as context manager, examples::

    with py.test.raises(ZeroDivisionError):
        x = 0
        1 / x

    with py.test.raises(RuntimeError) as excinfo:
        call_something()

    # you may do extra checks on excinfo.value|type|traceback here

  (thanks Ronny Pfannschmidt)

- Funcarg factories can now dynamically apply a marker to a
  test invocation.  This is for example useful if a factory
  provides parameters to a test which are expected-to-fail::

    def pytest_funcarg__arg(request):
        request.applymarker(py.test.mark.xfail(reason="flaky config"))
        ...

    def test_function(arg):
        ...

- improved error reporting on collection and import errors. This makes
  use of a more general mechanism, namely that for custom test item/collect
  nodes ``node.repr_failure(excinfo)`` is now uniformly called so that you can
  override it to return a string error representation of your choice
  which is going to be reported as a (red) string.

- introduce '--junitprefix=STR' option to prepend a prefix
  to all reports in the junitxml file.

Bug fixes / Maintenance
++++++++++++++++++++++++++

- make tests and the ``pytest_recwarn`` plugin in particular fully compatible
  to Python2.7 (if you use the ``recwarn`` funcarg warnings will be enabled so that
  you can properly check for their existence in a cross-python manner).
- refine --pdb: ignore xfailed tests, unify its TB-reporting and
  don't display failures again at the end.
- fix assertion interpretation with the ** operator (thanks Benjamin Peterson)
- fix issue105 assignment on the same line as a failing assertion (thanks Benjamin Peterson)
- fix issue104 proper escaping for test names in junitxml plugin (thanks anonymous)
- fix issue57 -f|--looponfail to work with xpassing tests (thanks Ronny)
- fix issue92 collectonly reporter and --pastebin (thanks Benjamin Peterson)
- fix py.code.compile(source) to generate unique filenames
- fix assertion re-interp problems on PyPy, by defering code
  compilation to the (overridable) Frame.eval class. (thanks Amaury Forgeot)
- fix py.path.local.pyimport() to work with directories
- streamline py.path.local.mkdtemp implementation and usage
- don't print empty lines when showing junitxml-filename
- add optional boolean ignore_errors parameter to py.path.local.remove
- fix terminal writing on win32/python2.4
- py.process.cmdexec() now tries harder to return properly encoded unicode objects
  on all python versions
- install plain py.test/py.which scripts also for Jython, this helps to
  get canonical script paths in virtualenv situations
- make path.bestrelpath(path) return ".", note that when calling
  X.bestrelpath the assumption is that X is a directory.
- make initial conftest discovery ignore "--" prefixed arguments
- fix resultlog plugin when used in an multicpu/multihost xdist situation
  (thanks Jakub Gustak)
- perform distributed testing related reporting in the xdist-plugin
  rather than having dist-related code in the generic py.test
  distribution
- fix homedir detection on Windows
- ship distribute_setup.py version 0.6.13

Changes between 1.3.0 and 1.3.1
==================================================

New features
++++++++++++++++++

- issue91: introduce new py.test.xfail(reason) helper
  to imperatively mark a test as expected to fail. Can
  be used from within setup and test functions. This is
  useful especially for parametrized tests when certain
  configurations are expected-to-fail.  In this case the
  declarative approach with the @py.test.mark.xfail cannot
  be used as it would mark all configurations as xfail.

- issue102: introduce new --maxfail=NUM option to stop
  test runs after NUM failures.  This is a generalization
  of the '-x' or '--exitfirst' option which is now equivalent
  to '--maxfail=1'.  Both '-x' and '--maxfail' will
  now also print a line near the end indicating the Interruption.

- issue89: allow py.test.mark decorators to be used on classes
  (class decorators were introduced with python2.6) and
  also allow to have multiple markers applied at class/module level
  by specifying a list.

- improve and refine letter reporting in the progress bar:
  .  pass
  f  failed test
  s  skipped tests (reminder: use for dependency/platform mismatch only)
  x  xfailed test (test that was expected to fail)
  X  xpassed test (test that was expected to fail but passed)

  You can use any combination of 'fsxX' with the '-r' extended
  reporting option. The xfail/xpass results will show up as
  skipped tests in the junitxml output - which also fixes
  issue99.

- make py.test.cmdline.main() return the exitstatus instead of raising
  SystemExit and also allow it to be called multiple times.  This of
  course requires that your application and tests are properly teared
  down and don't have global state.

Fixes / Maintenance
++++++++++++++++++++++

- improved traceback presentation:
  - improved and unified reporting for "--tb=short" option
  - Errors during test module imports are much shorter, (using --tb=short style)
  - raises shows shorter more relevant tracebacks
  - --fulltrace now more systematically makes traces longer / inhibits cutting

- improve support for raises and other dynamically compiled code by
  manipulating python's linecache.cache instead of the previous
  rather hacky way of creating custom code objects.  This makes
  it seemlessly work on Jython and PyPy where it previously didn't.

- fix issue96: make capturing more resilient against Control-C
  interruptions (involved somewhat substantial refactoring
  to the underlying capturing functionality to avoid race
  conditions).

- fix chaining of conditional skipif/xfail decorators - so it works now
  as expected to use multiple @py.test.mark.skipif(condition) decorators,
  including specific reporting which of the conditions lead to skipping.

- fix issue95: late-import zlib so that it's not required
  for general py.test startup.

- fix issue94: make reporting more robust against bogus source code
  (and internally be more careful when presenting unexpected byte sequences)


Changes between 1.2.1 and 1.3.0
==================================================

- deprecate --report option in favour of a new shorter and easier to
  remember -r option: it takes a string argument consisting of any
  combination of 'xfsX' characters.  They relate to the single chars
  you see during the dotted progress printing and will print an extra line
  per test at the end of the test run.  This extra line indicates the exact
  position or test ID that you directly paste to the py.test cmdline in order
  to re-run a particular test.

- allow external plugins to register new hooks via the new
  pytest_addhooks(pluginmanager) hook.  The new release of
  the pytest-xdist plugin for distributed and looponfailing
  testing requires this feature.

- add a new pytest_ignore_collect(path, config) hook to allow projects and
  plugins to define exclusion behaviour for their directory structure -
  for example you may define in a conftest.py this method::

        def pytest_ignore_collect(path):
            return path.check(link=1)

  to prevent even a collection try of any tests in symlinked dirs.

- new pytest_pycollect_makemodule(path, parent) hook for
  allowing customization of the Module collection object for a
  matching test module.

- extend and refine xfail mechanism:
  ``@py.test.mark.xfail(run=False)`` do not run the decorated test
  ``@py.test.mark.xfail(reason="...")`` prints the reason string in xfail summaries
  specifiying ``--runxfail`` on command line virtually ignores xfail markers

- expose (previously internal) commonly useful methods:
  py.io.get_terminal_with() -> return terminal width
  py.io.ansi_print(...) -> print colored/bold text on linux/win32
  py.io.saferepr(obj) -> return limited representation string

- expose test outcome related exceptions as py.test.skip.Exception,
  py.test.raises.Exception etc., useful mostly for plugins
  doing special outcome interpretation/tweaking

- (issue85) fix junitxml plugin to handle tests with non-ascii output

- fix/refine python3 compatibility (thanks Benjamin Peterson)

- fixes for making the jython/win32 combination work, note however:
  jython2.5.1/win32 does not provide a command line launcher, see
  http://bugs.jython.org/issue1491 . See pylib install documentation
  for how to work around.

- fixes for handling of unicode exception values and unprintable objects

- (issue87) fix unboundlocal error in assertionold code

- (issue86) improve documentation for looponfailing

- refine IO capturing: stdin-redirect pseudo-file now has a NOP close() method

- ship distribute_setup.py version 0.6.10

- added links to the new capturelog and coverage plugins


Changes between 1.2.1 and 1.2.0
=====================================

- refined usage and options for "py.cleanup"::

    py.cleanup     # remove "*.pyc" and "*$py.class" (jython) files
    py.cleanup -e .swp -e .cache # also remove files with these extensions
    py.cleanup -s  # remove "build" and "dist" directory next to setup.py files
    py.cleanup -d  # also remove empty directories
    py.cleanup -a  # synonym for "-s -d -e 'pip-log.txt'"
    py.cleanup -n  # dry run, only show what would be removed

- add a new option "py.test --funcargs" which shows available funcargs
  and their help strings (docstrings on their respective factory function)
  for a given test path

- display a short and concise traceback if a funcarg lookup fails

- early-load "conftest.py" files in non-dot first-level sub directories.
  allows to conveniently keep and access test-related options in a ``test``
  subdir and still add command line options.

- fix issue67: new super-short traceback-printing option: "--tb=line" will print a single line for each failing (python) test indicating its filename, lineno and the failure value

- fix issue78: always call python-level teardown functions even if the
  according setup failed.  This includes refinements for calling setup_module/class functions
  which will now only be called once instead of the previous behaviour where they'd be called
  multiple times if they raise an exception (including a Skipped exception).  Any exception
  will be re-corded and associated with all tests in the according module/class scope.

- fix issue63: assume <40 columns to be a bogus terminal width, default to 80

- fix pdb debugging to be in the correct frame on raises-related errors

- update apipkg.py to fix an issue where recursive imports might
  unnecessarily break importing

- fix plugin links

Changes between 1.2 and 1.1.1
=====================================

- moved dist/looponfailing from py.test core into a new
  separately released pytest-xdist plugin.

- new junitxml plugin: --junitxml=path will generate a junit style xml file
  which is processable e.g. by the Hudson CI system.

- new option: --genscript=path will generate a standalone py.test script
  which will not need any libraries installed.  thanks to Ralf Schmitt.

- new option: --ignore will prevent specified path from collection.
  Can be specified multiple times.

- new option: --confcutdir=dir will make py.test only consider conftest
  files that are relative to the specified dir.

- new funcarg: "pytestconfig" is the pytest config object for access
  to command line args and can now be easily used in a test.

- install 'py.test' and `py.which` with a ``-$VERSION`` suffix to
  disambiguate between Python3, python2.X, Jython and PyPy installed versions.

- new "pytestconfig" funcarg allows access to test config object

- new "pytest_report_header" hook can return additional lines
  to be displayed at the header of a test run.

- (experimental) allow "py.test path::name1::name2::..." for pointing
  to a test within a test collection directly.  This might eventually
  evolve as a full substitute to "-k" specifications.

- streamlined plugin loading: order is now as documented in
  customize.html: setuptools, ENV, commandline, conftest.
  also setuptools entry point names are turned to canonical namees ("pytest_*")

- automatically skip tests that need 'capfd' but have no os.dup

- allow pytest_generate_tests to be defined in classes as well

- deprecate usage of 'disabled' attribute in favour of pytestmark
- deprecate definition of Directory, Module, Class and Function nodes
  in conftest.py files.  Use pytest collect hooks instead.

- collection/item node specific runtest/collect hooks are only called exactly
  on matching conftest.py files, i.e. ones which are exactly below
  the filesystem path of an item

- change: the first pytest_collect_directory hook to return something
  will now prevent further hooks to be called.

- change: figleaf plugin now requires --figleaf to run.  Also
  change its long command line options to be a bit shorter (see py.test -h).

- change: pytest doctest plugin is now enabled by default and has a
  new option --doctest-glob to set a pattern for file matches.

- change: remove internal py._* helper vars, only keep py._pydir

- robustify capturing to survive if custom pytest_runtest_setup
  code failed and prevented the capturing setup code from running.

- make py.test.* helpers provided by default plugins visible early -
  works transparently both for pydoc and for interactive sessions
  which will regularly see e.g. py.test.mark and py.test.importorskip.

- simplify internal plugin manager machinery
- simplify internal collection tree by introducing a RootCollector node

- fix assert reinterpreation that sees a call containing "keyword=..."

- fix issue66: invoke pytest_sessionstart and pytest_sessionfinish
  hooks on slaves during dist-testing, report module/session teardown
  hooks correctly.

- fix issue65: properly handle dist-testing if no
  execnet/py lib installed remotely.

- skip some install-tests if no execnet is available

- fix docs, fix internal bin/ script generation


Changes between 1.1.1 and 1.1.0
=====================================

- introduce automatic plugin registration via 'pytest11'
  entrypoints via setuptools' pkg_resources.iter_entry_points

- fix py.test dist-testing to work with execnet >= 1.0.0b4

- re-introduce py.test.cmdline.main() for better backward compatibility

- svn paths: fix a bug with path.check(versioned=True) for svn paths,
  allow '%' in svn paths, make svnwc.update() default to interactive mode
  like in 1.0.x and add svnwc.update(interactive=False) to inhibit interaction.

- refine distributed tarball to contain test and no pyc files

- try harder to have deprecation warnings for py.compat.* accesses
  report a correct location

Changes between 1.1.0 and 1.0.2
=====================================

* adjust and improve docs

* remove py.rest tool and internal namespace - it was
  never really advertised and can still be used with
  the old release if needed.  If there is interest
  it could be revived into its own tool i guess.

* fix issue48 and issue59: raise an Error if the module
  from an imported test file does not seem to come from
  the filepath - avoids "same-name" confusion that has
  been reported repeatedly

* merged Ronny's nose-compatibility hacks: now
  nose-style setup_module() and setup() functions are
  supported

* introduce generalized py.test.mark function marking

* reshuffle / refine command line grouping

* deprecate parser.addgroup in favour of getgroup which creates option group

* add --report command line option that allows to control showing of skipped/xfailed sections

* generalized skipping: a new way to mark python functions with skipif or xfail
  at function, class and modules level based on platform or sys-module attributes.

* extend py.test.mark decorator to allow for positional args

* introduce and test "py.cleanup -d" to remove empty directories

* fix issue #59 - robustify unittest test collection

* make bpython/help interaction work by adding an __all__ attribute
  to ApiModule, cleanup initpkg

* use MIT license for pylib, add some contributors

* remove py.execnet code and substitute all usages with 'execnet' proper

* fix issue50 - cached_setup now caches more to expectations
  for test functions with multiple arguments.

* merge Jarko's fixes, issue #45 and #46

* add the ability to specify a path for py.lookup to search in

* fix a funcarg cached_setup bug probably only occuring
  in distributed testing and "module" scope with teardown.

* many fixes and changes for making the code base python3 compatible,
  many thanks to Benjamin Peterson for helping with this.

* consolidate builtins implementation to be compatible with >=2.3,
  add helpers to ease keeping 2 and 3k compatible code

* deprecate py.compat.doctest|subprocess|textwrap|optparse

* deprecate py.magic.autopath, remove py/magic directory

* move pytest assertion handling to py/code and a pytest_assertion
  plugin, add "--no-assert" option, deprecate py.magic namespaces
  in favour of (less) py.code ones.

* consolidate and cleanup py/code classes and files

* cleanup py/misc, move tests to bin-for-dist

* introduce delattr/delitem/delenv methods to py.test's monkeypatch funcarg

* consolidate py.log implementation, remove old approach.

* introduce py.io.TextIO and py.io.BytesIO for distinguishing between
  text/unicode and byte-streams (uses underlying standard lib io.*
  if available)

* make py.unittest_convert helper script available which converts "unittest.py"
  style files into the simpler assert/direct-test-classes py.test/nosetests
  style.  The script was written by Laura Creighton.

* simplified internal localpath implementation

Changes between 1.0.1 and 1.0.2
=====================================

* fixing packaging issues, triggered by fedora redhat packaging,
  also added doc, examples and contrib dirs to the tarball.

* added a documentation link to the new django plugin.

Changes between 1.0.0 and 1.0.1
=====================================

* added a 'pytest_nose' plugin which handles nose.SkipTest,
  nose-style function/method/generator setup/teardown and
  tries to report functions correctly.

* capturing of unicode writes or encoded strings to sys.stdout/err
  work better, also terminalwriting was adapted and somewhat
  unified between windows and linux.

* improved documentation layout and content a lot

* added a "--help-config" option to show conftest.py / ENV-var names for
  all longopt cmdline options, and some special conftest.py variables.
  renamed 'conf_capture' conftest setting to 'option_capture' accordingly.

* fix issue #27: better reporting on non-collectable items given on commandline
  (e.g. pyc files)

* fix issue #33: added --version flag (thanks Benjamin Peterson)

* fix issue #32: adding support for "incomplete" paths to wcpath.status()

* "Test" prefixed classes are *not* collected by default anymore if they
  have an __init__ method

* monkeypatch setenv() now accepts a "prepend" parameter

* improved reporting of collection error tracebacks

* simplified multicall mechanism and plugin architecture,
  renamed some internal methods and argnames

Changes between 1.0.0b9 and 1.0.0
=====================================

* more terse reporting try to show filesystem path relatively to current dir
* improve xfail output a bit

Changes between 1.0.0b8 and 1.0.0b9
=====================================

* cleanly handle and report final teardown of test setup

* fix svn-1.6 compat issue with py.path.svnwc().versioned()
  (thanks Wouter Vanden Hove)

* setup/teardown or collection problems now show as ERRORs
  or with big "E"'s in the progress lines.  they are reported
  and counted separately.

* dist-testing: properly handle test items that get locally
  collected but cannot be collected on the remote side - often
  due to platform/dependency reasons

* simplified py.test.mark API - see keyword plugin documentation

* integrate better with logging: capturing now by default captures
  test functions and their immediate setup/teardown in a single stream

* capsys and capfd funcargs now have a readouterr() and a close() method
  (underlyingly py.io.StdCapture/FD objects are used which grew a
  readouterr() method as well to return snapshots of captured out/err)

* make assert-reinterpretation work better with comparisons not
  returning bools (reported with numpy from thanks maciej fijalkowski)

* reworked per-test output capturing into the pytest_iocapture.py plugin
  and thus removed capturing code from config object

* item.repr_failure(excinfo) instead of item.repr_failure(excinfo, outerr)


Changes between 1.0.0b7 and 1.0.0b8
=====================================

* pytest_unittest-plugin is now enabled by default

* introduced pytest_keyboardinterrupt hook and
  refined pytest_sessionfinish hooked, added tests.

* workaround a buggy logging module interaction ("closing already closed
  files").  Thanks to Sridhar Ratnakumar for triggering.

* if plugins use "py.test.importorskip" for importing
  a dependency only a warning will be issued instead
  of exiting the testing process.

* many improvements to docs:
  - refined funcargs doc , use the term "factory" instead of "provider"
  - added a new talk/tutorial doc page
  - better download page
  - better plugin docstrings
  - added new plugins page and automatic doc generation script

* fixed teardown problem related to partially failing funcarg setups
  (thanks MrTopf for reporting), "pytest_runtest_teardown" is now
  always invoked even if the "pytest_runtest_setup" failed.

* tweaked doctest output for docstrings in py modules,
  thanks Radomir.

Changes between 1.0.0b3 and 1.0.0b7
=============================================

* renamed py.test.xfail back to py.test.mark.xfail to avoid
  two ways to decorate for xfail

* re-added py.test.mark decorator for setting keywords on functions
  (it was actually documented so removing it was not nice)

* remove scope-argument from request.addfinalizer() because
  request.cached_setup has the scope arg. TOOWTDI.

* perform setup finalization before reporting failures

* apply modified patches from Andreas Kloeckner to allow
  test functions to have no func_code (#22) and to make
  "-k" and function keywords work  (#20)

* apply patch from Daniel Peolzleithner (issue #23)

* resolve issue #18, multiprocessing.Manager() and
  redirection clash

* make __name__ == "__channelexec__" for remote_exec code

Changes between 1.0.0b1 and 1.0.0b3
=============================================

* plugin classes are removed: one now defines
  hooks directly in conftest.py or global pytest_*.py
  files.

* added new pytest_namespace(config) hook that allows
  to inject helpers directly to the py.test.* namespace.

* documented and refined many hooks

* added new style of generative tests via
  pytest_generate_tests hook that integrates
  well with function arguments.


Changes between 0.9.2 and 1.0.0b1
=============================================

* introduced new "funcarg" setup method,
  see doc/test/funcarg.txt

* introduced plugin architecuture and many
  new py.test plugins, see
  doc/test/plugins.txt

* teardown_method is now guaranteed to get
  called after a test method has run.

* new method: py.test.importorskip(mod,minversion)
  will either import or call py.test.skip()

* completely revised internal py.test architecture

* new py.process.ForkedFunc object allowing to
  fork execution of a function to a sub process
  and getting a result back.

XXX lots of things missing here XXX

Changes between 0.9.1 and 0.9.2
===============================

* refined installation and metadata, created new setup.py,
  now based on setuptools/ez_setup (thanks to Ralf Schmitt
  for his support).

* improved the way of making py.* scripts available in
  windows environments, they are now added to the
  Scripts directory as ".cmd" files.

* py.path.svnwc.status() now is more complete and
  uses xml output from the 'svn' command if available
  (Guido Wesdorp)

* fix for py.path.svn* to work with svn 1.5
  (Chris Lamb)

* fix path.relto(otherpath) method on windows to
  use normcase for checking if a path is relative.

* py.test's traceback is better parseable from editors
  (follows the filenames:LINENO: MSG convention)
  (thanks to Osmo Salomaa)

* fix to javascript-generation, "py.test --runbrowser"
  should work more reliably now

* removed previously accidentally added
  py.test.broken and py.test.notimplemented helpers.

* there now is a py.__version__ attribute

Changes between 0.9.0 and 0.9.1
===============================

This is a fairly complete list of changes between 0.9 and 0.9.1, which can
serve as a reference for developers.

* allowing + signs in py.path.svn urls [39106]
* fixed support for Failed exceptions without excinfo in py.test [39340]
* added support for killing processes for Windows (as well as platforms that
  support os.kill) in py.misc.killproc [39655]
* added setup/teardown for generative tests to py.test [40702]
* added detection of FAILED TO LOAD MODULE to py.test [40703, 40738, 40739]
* fixed problem with calling .remove() on wcpaths of non-versioned files in
  py.path [44248]
* fixed some import and inheritance issues in py.test [41480, 44648, 44655]
* fail to run greenlet tests when pypy is available, but without stackless
  [45294]
* small fixes in rsession tests [45295]
* fixed issue with 2.5 type representations in py.test [45483, 45484]
* made that internal reporting issues displaying is done atomically in py.test
  [45518]
* made that non-existing files are igored by the py.lookup script [45519]
* improved exception name creation in py.test [45535]
* made that less threads are used in execnet [merge in 45539]
* removed lock required for atomical reporting issue displaying in py.test
  [45545]
* removed globals from execnet [45541, 45547]
* refactored cleanup mechanics, made that setDaemon is set to 1 to make atexit
  get called in 2.5 (py.execnet) [45548]
* fixed bug in joining threads in py.execnet's servemain [45549]
* refactored py.test.rsession tests to not rely on exact output format anymore
  [45646]
* using repr() on test outcome [45647]
* added 'Reason' classes for py.test.skip() [45648, 45649]
* killed some unnecessary sanity check in py.test.collect [45655]
* avoid using os.tmpfile() in py.io.fdcapture because on Windows it's only
  usable by Administrators [45901]
* added support for locking and non-recursive commits to py.path.svnwc [45994]
* locking files in py.execnet to prevent CPython from segfaulting [46010]
* added export() method to py.path.svnurl
* fixed -d -x in py.test [47277]
* fixed argument concatenation problem in py.path.svnwc [49423]
* restore py.test behaviour that it exits with code 1 when there are failures
  [49974]
* don't fail on html files that don't have an accompanying .txt file [50606]
* fixed 'utestconvert.py < input' [50645]
* small fix for code indentation in py.code.source [50755]
* fix _docgen.py documentation building [51285]
* improved checks for source representation of code blocks in py.test [51292]
* added support for passing authentication to py.path.svn* objects [52000,
  52001]
* removed sorted() call for py.apigen tests in favour of [].sort() to support
  Python 2.3 [52481]
