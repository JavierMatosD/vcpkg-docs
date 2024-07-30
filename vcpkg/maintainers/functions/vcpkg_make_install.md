---
title: vcpkg_make_install
description: Use vcpkg_make_install to build and install a Make-based project.
ms.date: 01/31/2024
---
# vcpkg_make_install

Build and install a Make-based project.

## Usage

```cmake
vcpkg_make_install(
    [DISABLE_PARALLEL]
    [DISABLE_DESTDIR]
    [DISABLE_MSVC_FLAG_ESCAPING]
    [USE_RESPONSE_FILES]
    [LOGFILE_ROOT <root-name>]
    [SUBPATH <sub-directory>]
    [MAKEFILE <makefile-name>]
    [TARGETS <target-name>...]
    [OPTIONS <make-option>...]
    [OPTIONS_RELEASE <make-option>...]
    [OPTIONS_DEBUG <make-option>...]
)
```

To use this function, you must depend on the helper port `vcpkg-make`:

```json
"dependencies": [
  {
    "name": "vcpkg-make",
    "host": true
  }
]
```

## Parameters

### ADD_BIN_TO_PATH

Adds the configure dependent `(debug/)bin` directory to the system path. This is useful if configure builds and runs executables with shared dependencies.

### DISABLE_PARALLEL

By default, `vcpkg_make_install` will run make with the `-j` option to enable parallel building. If your project does not support parallel builds or you encounter issues with it, set this flag to disable parallel building. This will cause make to be executed without the -j option, running build steps sequentially.

### DISABLE_DESTDIR

By default, `make install` will use the `DESTDIR` variable to redirect installation to the package directory. Use this flag if `DESTDIR` should not be set.

### DISABLE_MSVC_FLAG_ESCAPING

Prevents escaping of MSVC flags. Use this if the project's makefiles do not expect escaped flags.

### USE_RESPONSE_FILES

Enables the use of response files for passing arguments to `make`, circumventing command line length limits on some platforms.

### LOGFILE_ROOT

Specifies the base name for log files generated by the build. Defaults to "make".

### SUBPATH

Specifies a sub-directory within the working directory where the makefile is located or where the build should be executed. If not set, it defaults to an empty string, meaning the build is executed directly in the working directory.

### MAKEFILE

Specifies the name of the makefile to use. Defaults to "Makefile".

### TARGETS

Specifies the targets to pass to make. Defaults to "all;install".

### SHELL

Specifies the shell to use for running `make`. Useful for environments where the default shell might not be compatible with the makefiles.

### OPTIONS

Additional options to pass to `make` during the build.

### OPTIONS_RELEASE

Additional options to pass to `make` during the release build.

### OPTIONS_DEBUG

Additional options to pass to `make` during the debug build.

## Examples

```cmake
vcpkg_from_github(OUT_SOURCE_PATH source_path ...)
vcpkg_make_configure(SOURCE_PATH "${source_path}")
vcpkg_make_install()
```

## Remarks

This command replaces [`vcpkg_install_make()`](vcpkg_install_make.md).