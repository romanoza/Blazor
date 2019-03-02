# Upgrading Mono Linker

* `git clone https://github.com/mono/linker.git`
* `cd linker`
* `git submodule update --init --recursive`
* `cd corebuild`
* `set VS150COMNTOOLS=c:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\Tools\` (or whatever is your installation path for VS2017, though not strictly certain you need this step)
* `./dotnet.{sh/cmd} restore ./integration/linker.sln`
* `./dotnet.{sh/cmd} pack ./integration/ILLink.Tasks/ILLink.Tasks.csproj -c Release`
* `cd integration/bin/nupkgs`

In here you'll now have a `.nupkg` file. Extract its files (i.e., treating it as a `.zip` file), open its `tools/netcoreapp2.0` directory, and copy the following to `(blazorroot)/mono/tools/binaries/illink`:

* `illink.dll`
* `Mono.Cecil.dll`
* `Mono.Cecil.Mdb.dll`
* `Mono.Cecil.Pdb.dll`

Presumably you should also copy any other new dependencies it has, though it's not necessary to copy `NuGet.*.dll` or `Newtonsoft.Json.dll` or the `runtimes` subdirectory (since we execute it as a framework-dependent app).

Note that `(blazorroot)/mono/tools/binaries/illink` also contains `illink.runtimeconfig.json`, which is necessary for `dotnet illink.dll` to work.
