This is a very quick-and-dirty attempt to reproduce the error described in the WiX problem report
[here](https://github.com/wixtoolset/issues/issues/8114).

The installed application (AppToBeIncluded) is completely bogus and likely won't even run. It
is only present to demonstrate how the version information for both the MSI (MainPackage), and
the bundle (BundleContainingMainPackage) is propagated from the application in question.

The repository contains two changesets. The initial one uses Wix 4.0.5. It should be possible
to build it from within Visual Studio (I'm using Microsoft Visual Studio Professional 2022 (64-bit),
Version 17.9.5) without errors.

The second changeset changes the WiX references from 4.0.5 to 5.0.0. Within Visual Studio, this
then causes a WIX8001 error.

Curiously, the error does not appear to occur if triggering the build by using `dotnet build`.

In the initial (private) environment which triggered the creation of the case, the MSBuild processing
is triggered from within a [Cake](https://cakebuild.net/) script, which leads me to wonder if the problem
only manifests if WiX is running in an environment where MSBuild is not the main parent process.