# osslsigncode_vc140

Windows / Visual Studio 2015 (`v140`) packaging of an `osslsigncode` source snapshot.

This repository exists to keep a small Windows buildable version of
`osslsigncode` together with the Visual Studio project files and compatibility
glue needed for that environment.

## What Is In This Repository

- `osslsigncode_vc140/osslsigncode.c`
  - bundled `osslsigncode` source snapshot
- `osslsigncode_vc140/osslsigncode_vc140.vcxproj`
  - Visual Studio 2015 project file
- `osslsigncode_vc140/unistd.h`
  - small Windows compatibility shim
- `osslsigncode_vc140/packages.config`
  - NuGet package references for OpenSSL and zlib
- `osslsigncode_vc140.sln`
  - Visual Studio solution

This repository is best treated as a historical Windows port / build wrapper,
not as a cleanly synchronized upstream mirror.

## Why This Exists

`osslsigncode` is an OpenSSL-based tool for Authenticode signing and
verification of PE, MSI, and CAB files.

This repository packages a source snapshot so it can be opened and built on
Windows with Visual Studio 2015 (`v140`), including a small `unistd.h`
compatibility layer for the Windows build path.

## Build

Prerequisites:

- Visual Studio 2015 with C++ tools (`v140`)
- Windows 8.1 SDK
- NuGet package restore enabled

Build steps:

1. Open `osslsigncode_vc140.sln` in Visual Studio 2015.
2. Restore NuGet packages referenced by `osslsigncode_vc140/packages.config`.
3. Build `Release|Win32` or `Release|x64`.

Project configuration currently includes:

- `Debug|Win32`
- `Release|Win32`
- `Debug|x64`
- `Release|x64`

## Usage

The bundled source snapshot exposes commands such as:

- `sign`
- `extract-signature`
- `remove-signature`
- `verify`

Example:

```bash
osslsigncode verify -in somefile.exe
```

## Attribution And Licensing

Current upstream project:

- https://github.com/mtrojnar/osslsigncode

The bundled `osslsigncode_vc140/osslsigncode.c` file includes the copyright and
license header present in that bundled source file.

The file header states that the bundled source is GPL v3 or later, with an
OpenSSL linking exception. Review the source header carefully before
redistributing modified source or binaries.

The bundled source header also credits Per Allansson. This repository keeps a
Windows-oriented packaging of a bundled source snapshot and does not claim to be
the canonical upstream project.

For current releases, maintenance status, and upstream history, refer to the
upstream project link above.

## Notes

- The repository history is minimal.
- The tree is intentionally small and focused on the Windows build path.
- IDE-local files are excluded so the repository stays usable as a shared
  reference repository.
