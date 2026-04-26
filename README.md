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

## Provenance

Upstream reference:

- https://github.com/mtrojnar/osslsigncode

The bundled `osslsigncode_vc140/osslsigncode.c` file is a source snapshot, not
a git submodule or subtree. The local git history imports it as a complete file
and does not identify an exact upstream commit, tag, or release archive.

The source file itself carries this RCS identifier:

```text
osslsigncode.c,v 1.7.1 2014/07/11 14:14:14 mfive
```

Treat that identifier and the file header as the available in-tree provenance
for the bundled source. Before redistributing a public build or making security
claims, compare this snapshot against the upstream project or a known release.

## Licensing Context

The bundled `osslsigncode_vc140/osslsigncode.c` file includes the copyright and
license header present in that source snapshot.

That file header states that the bundled source is licensed under the GNU
General Public License version 3 or, at your option, any later version, with a
special OpenSSL linking exception. The exception text is part of the source
header; it does not remove the GPL obligations for code used other than
OpenSSL.

A copy of the GPLv3 text referenced by the source header is provided in
`COPYING.GPL-3.0`. That file is the GPL text only; it does not replace the
OpenSSL exception or any file-specific notices.

The bundled source header credits Per Allansson. This repository does not claim
to be the canonical upstream project.

The Visual Studio project references third-party NuGet packages:

- `rmt_openssl` `1.0.2.6`
- `rmt_zlib` `1.2.8.5`

Those package references are not vendored source in this repository. Review the
third-party package licenses and support status separately before distributing
binaries.

## Local VC140 Scope

This repository is the local Windows / Visual Studio 2015 (`v140`) packaging
layer around the bundled source snapshot. The in-tree VC140-specific scope is:

- Visual Studio solution and project files
- NuGet package references for OpenSSL and zlib
- `osslsigncode_vc140/unistd.h`, a small Windows compatibility shim

The repository does not currently document a complete diff between the bundled
`osslsigncode.c` and any upstream release. Do not treat the C file as pristine
upstream source without doing that comparison.

## Notes

- The repository history is minimal.
- The tree is intentionally small and focused on the Windows build path.
- IDE-local files are excluded so the repository stays usable as a shared
  reference repository.
