[![NuGet Version](https://img.shields.io/nuget/v/Drastic.PureLayout.svg)](https://www.nuget.org/packages/Drastic.PureLayout/) ![License](https://img.shields.io/badge/License-MIT-blue.svg)

# Drastic.PureLayout

Drastic.PureLayout is binding of [PureLayout](https://github.com/PureLayout/PureLayout), a layout library for iOS and macOS that enables helper extension methods for handling Auto Layout. While there is an existing binding available with [PureLayout.Net](https://github.com/mallibone/PureLayout.Net), this version contains some new features.

- In addition to the existing iOS and Mac targets, Drastic.PureLayout includes Mac Catalyst and tvOS bindings.
- Drastic.PureLayout removes the legacy Xamarin bindings and replaces them with modern `dotnet` versions. This is a drop-in replacement for the PureLayout.Net versions. Switch out the nuget, replace the namespace, and it should work the same.

# Setup

Include the Nuget in your iOS/macOS/tvOS project

```powershell
Install-Package Drastic.PureLayout
```

The nuget comes with the PureLayout framework bundled in.

# Howto

The documentation for [PureLayout.Net](https://github.com/mallibone/PureLayout.Net/blob/master/README.md) also applies to this library. The only difference is the namespace.

# Building

To build Drastic.PureLayout

- Clone the repo with `git clone --recursive https://github.com/drasticactions/Drastic.PureLayout.git`
- Run `make` in the root directory.

This should compile PureLayout, build the xcframework, and build the binding.

# Pack the nuget

Build the project, then run `make pack`. This will create the nuget package. The version number is currently contained with `src/Directory.Build.Props`.