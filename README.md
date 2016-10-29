# nenv-vars

This is a plugin for [nenv](https://github.com/ryuone/nenv)
that lets you set global and project-specific environment variables
before spawning Ruby processes.

nenv-vars is based on [rbenv-vars](https://github.com/sstephenson/rbenv-vars)
by Sam Stephenson.

## Installation

Make sure you have the latest version of nenv, then run:

    git clone https://github.com/madumlao/nenv-vars.git $(rbenv root)/plugins/nenv-vars

## Usage

Define environment variables in an `.nenv-vars` file in your project,
one variable per line, in the format `VAR=value`. For example:

    CLASSPATH=src:lib/foo.jar

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `CLASSPATH`:

    CLASSPATH=src:lib/foo.jar:$CLASSPATH

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

    JAVA_OPTS?=-server -Xmx768m -Xms768m -Xmn128m -Xss20m

In the above case, `JAVA_OPTS` will only be set if `$JAVA_OPTS` is
currently empty (i.e., if `[ -z "$JAVA_OPTS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.nenv/vars` file will be set
first. Then variables specified in `.nenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.nenv-vars` file in the current directory are set last.

Use the `nenv vars` command to print all environment variables in the
order they'll be set.

## Version History (nenv)

**1.2.0.2 (October 30, 2016)

* Adapted jenv-vars for nenv.

## Version History (jenv)

**1.2.0.1 (February 26, 2015)

* Adapted rbenv-vars for jenv.

## Version History (rbenv)

**1.2.0** (January 9, 2013)

* Fixed a bug where source files without a trailing newline could
  concatenate improperly with other source files on systems with GNU
  sed.
* Changed the output of `rbenv vars` to include the source file path
  in a comment above its variables, and an empty line between each
  source file, for easier debugging.
* Added support for `rbenv help vars` with jenv 0.4.0.

**1.1.0** (June 25, 2012)

* Added support for conditional variable assignments using
  `?=`. Thanks to Scott Gonyea for the patch.

**1.0.0** (September 27, 2011)

* Initial public release.

## License

&copy; 2015 Mark David Dumlao. Released under the MIT license. See
`LICENSE` for details.
