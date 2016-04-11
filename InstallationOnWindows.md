﻿#summary Installation of mod\_wsgi on Windows.

_**If you are using mod\_wsgi, please consider making a
[donation](HowToContributeBack.md).**_

# Installation On Windows #

If using Windows you can use the precompiled binaries available for
download or compile from source code. Only mod\_wsgi 3.0 and later provides
the required makefiles for building from source code on Windows however.

## Module Installation ##

The appropriate `mod_wsgi.so` file for the version of Python and Apache
being used should be copied into the Apache modules directory. For Apache
2.2, this would typically be directory:

```
/Program Files/Apache Software Foundation/Apache22/modules
```

Ensure first that this is actually the location where Apache has been
installed in case it is different for your platform. Also ensure that the
file when installed has access permissions such that the user that the
Apache service runs as will be able to read it.

To configure Apache to make use of mod\_wsgi, follow the instructions for
loading mod\_wsgi in the [Quick Installation Guide](QuickInstallationGuide.md).
Also refer to the [Quick Configuration Guide](QuickConfigurationGuide.md) and
[Configuration Guidelines](ConfigurationGuidelines.md).

Note that the binaries from this site aren't actually called 'mod\_wsgi.so'.
You should rename the file to 'mod\_wsgi.so' when it is placed into the
Apache modules directory, or modify as appropriate the LoadModule line
you add to the Apache configuration file to refer to its actual name.

Also, the binaries from this site will have been compiled against the
latest version of Apache available at the time. If you are using an older
patch revision of Apache, it is possible that you may have problems. Ensure
therefore that you always update to latest version of Apache.

## Compiling From Source Code ##

To compile from source code you will need Microsoft C/C++ compiler for
Windows. This must be the same version of the compiler as used to build the
version of Python being used. The free express editions of the compilers
can be used.

The mod\_wsgi source code however only supplies makefiles for the
latest available version of Microsoft C/C++ compiler and the versions of
Python that use it.

You can obtain this version of the Microsoft C/C++ compiler from:

> http://www.microsoft.com/express/vc/

Once you have unpacked the mod\_wsgi source code, you should open up the
Visual Studio developer command shell and change to the directory where you
unpacked the source code. If you have Apache 2.2 and Python 2.6 installed,
run:

```
nmake -f win32-ap22py26.mk
```

If you have Apache 2.2 and Python 3.1 installed, run:

```
nmake -f win32-ap22py31.mk
```

The result of this will be a 'mod\_wsgi.so' file. This will need to be
copied into the Apache modules directory by hand.

To clean up, run:

```
nmake -f win32-ap22py26.mk clean
```

If needing to use other versions of Apache or Python you will need to copy
the makefiles and modify as appropriate, remembering that for older versions
of Python you will need the older Microsoft C/C++ compiler it requires.

## Python Requirements ##

When Python was being installed, it should be installed as an Administrator
and it must be made avaiable to all users. By installing it as an
Administrator, it will ensure that the required C library DLL is installed
into the Windows system folder and will be able to be found by Apache when
it is being run as a service.

Running installation of Python as the Administrator and making it available
to all users also ensures that Windows registry entries related to Python
are configured for the entire machine and not just the user that installed
Python.

Note that if you use the non-interactive installer for Python, it will
default to installing Python only for the current user. To ensure it is
installed for all users, then ALLUSERS=1 must be set appropriately in the
installer configuration.

If you have multiple versions of Python installed on your system, you must
ensure that the first one found when the application PATH is searched is
the version you wish to use. If this isn't the case, Python may not find
the correct directories from which to load the site initialisation file and
any Python modules.

Note that although the precompiled mod\_wsgi modules may not have been
compiled with the exact same patch level version of Python as you are
running, and as a result you may see a warning in the Apache error log
files about a version mismatch, this warning can be ignored. You should
only be concerned where the major/minor versions of Python differ, in
which case you should install the correct version of the precompiled
mod\_wsgi module binary.