% KCONFIG-gettext(1) kconfig-gettext Man Page
% Philippe Thierry
% October 2017
# NAME
kconfig-gettext - Standalone implementation of the Linux Kconfig parser

# SYNOPSIS
**kconfig-gettext [options] <KConfig_file>**

# DESCRIPTION

The kconfig toolkit support the Kconfig language and implement
the parser and the configuration support associated to the KConfig
files respecting the Linux kernel KConfig convention.

At configuration time:

 - kconfig-mconf is based on ncurses (menuconfig)
 - kconfig-conf is based on dialog (config)
 - kconfig-gconf is based on GTK+ (gconfig)

Associated tools:

 - kconfig-diff displays symbols diff between .config files

# OPTIONS

**--silentoldconfig**
Only for kconfig-conf, reload a given .config and regenerate
header and command files accordingly.

**--allnoconfig**
Set all boolean configuration to no.

**--allyesconfig**
Set all boolean configuration to yes.

**--randconfig**
Generates a random configuration.

# ENVIRONMENT

## Environment variables for '*config'

**KCONFIG_CONFIG**

This environment variable can be used to specify a default kernel config
file name to override the default name of ".config".

**KCONFIG_OVERWRITECONFIG**

If you set KCONFIG_OVERWRITECONFIG in the environment, Kconfig will not
break symlinks when .config is a symlink to somewhere else.

**CONFIG_**

If you set CONFIG_ in the environment, Kconfig will prefix all symbols
with its value when saving the configuration, instead of using the default,
"CONFIG_".

## Environment variables for '{allyes/allmod/allno/rand}config'

**KCONFIG_ALLCONFIG**

The allyesconfig/allmodconfig/allnoconfig/randconfig variants can also
use the environment variable KCONFIG_ALLCONFIG as a flag or a filename
that contains config symbols that the user requires to be set to a
specific value.  If KCONFIG_ALLCONFIG is used without a filename where
KCONFIG_ALLCONFIG == "" or KCONFIG_ALLCONFIG == "1", "make *config"
checks for a file named "all{yes/mod/no/def/random}.config"
(corresponding to the *config command that was used) for symbol values
that are to be forced.  If this file is not found, it checks for a
file named "all.config" to contain forced values.

This enables you to create "miniature" config (miniconfig) or custom
config files containing just the config symbols that you are interested
in.  Then the kernel config system generates the full .config file,
including symbols of your miniconfig file.

This 'KCONFIG_ALLCONFIG' file is a config file which contains
(usually a subset of all) preset config symbols.  These variable
settings are still subject to normal dependency checks.

Examples:
	KCONFIG_ALLCONFIG=custom-notebook.config make allnoconfig
or
	KCONFIG_ALLCONFIG=mini.config make allnoconfig
or
	make KCONFIG_ALLCONFIG=mini.config allnoconfig

These examples will disable most options (allnoconfig) but enable or
disable the options that are explicitly listed in the specified
mini-config files.

## Environment variables for 'randconfig'

**KCONFIG_SEED**

You can set this to the integer value used to seed the RNG, if you want
to somehow debug the behaviour of the kconfig parser/frontends.
If not set, the current time will be used. 


**KCONFIG_PROBABILITY**

This variable can be used to skew the probabilities.
See /usr/share/doc/kconfig-frontends/kconfig.txt.gz.


Environment variables for 'silentoldconfig'

**KCONFIG_NOSILENTUPDATE**

If this variable has a non-blank value, it prevents silent kernel
config updates (requires explicit updates).

**KCONFIG_AUTOCONFIG**

This environment variable can be set to specify the path & name of the
"auto.conf" file.  Its default value is "include/config/auto.conf".

**KCONFIG_TRISTATE**

This environment variable can be set to specify the path & name of the
"tristate.conf" file.  Its default value is "include/config/tristate.conf".

**KCONFIG_AUTOHEADER**

This environment variable can be set to specify the path & name of the
"autoconf.h" (header) file.
Its default value is "include/generated/autoconf.h".


# HISTORY

June 2017, Man page originally compiled by Philippe Thierry (phil at reseau-libre dot
com)
