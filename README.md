Demo to help demonstrate the problem described at http://www.opclabs.com/forum/feature-requests-product-improvement-ideas/2523-please-support-packagereference-for-nuget-packages . This project uses `<PackageReference/>` to reference [`OpcLabs.QuickOpc`](https://www.nuget.org/packages/OpcLabs.QuickOpc/5.53.315). As a result, when compiled, the project is missing the following files which are (in my tests) required for successful execution:

* `App_Web_OpcLabs.EasyOpcClassicRaw.amd64.dll`
* `App_Web_OpcLabs.EasyOpcClassicRaw.x86.dll`

The result is that the program crashes if you simply compile and run this project without having first installed OpcLabs.QuickOpc via the installer. You get a stack like the following:

```
Unhandled Exception: System.TypeInitializationException: The type initializer for 'OpcLabs.EasyOpc.DataAccess.EasyDAClient' threw an exception. ---> System.IO.FileNotFoundException: Could not load file or assembly 'App_Web_OpcLabs.EasyOpcClassicRaw.x86, Version=5.53.315.1, Culture=neutral, PublicKeyToken=6faddca41dacb409' or one of its dependencies. The system cannot find the file specified.
+ It is possible that Microsoft Visual C++ Redistributable Package is not installed.
   at System.Reflection.RuntimeAssembly._nLoad(AssemblyName fileName, String codeBase, Evidence assemblySecurity, RuntimeAssembly locationHint, StackCrawlMark& stackMark, IntPtr pPrivHostBinder, Boolean throwOnFileNotFound, Boolean forIntrospection, Boolean suppressSecurityChecks)
   at System.Reflection.RuntimeAssembly.nLoad(AssemblyName fileName, String codeBase, Evidence assemblySecurity, RuntimeAssembly locationHint, StackCrawlMark& stackMark, IntPtr pPrivHostBinder, Boolean throwOnFileNotFound, Boolean forIntrospection, Boolean suppressSecurityChecks)
   at System.Reflection.RuntimeAssembly.InternalLoadAssemblyName(AssemblyName assemblyRef, Evidence assemblySecurity, RuntimeAssembly reqAssembly, StackCrawlMark& stackMark, IntPtr pPrivHostBinder, Boolean throwOnFileNotFound, Boolean forIntrospection, Boolean suppressSecurityChecks)
   at System.Reflection.RuntimeAssembly.InternalLoad(String assemblyString, Evidence assemblySecurity, StackCrawlMark& stackMark, IntPtr pPrivHostBinder, Boolean forIntrospection)
   at System.Reflection.RuntimeAssembly.InternalLoad(String assemblyString, Evidence assemblySecurity, StackCrawlMark& stackMark, Boolean forIntrospection)
   at System.Reflection.Assembly.Load(String assemblyString)
   at OpcLabs.EasyOpc.Implementations.Native.Assemblies.LoadRawAssembly(String name)
   at OpcLabs.EasyOpc.Implementations.Native.Assemblies.get_EasyOpcClassicRaw()
   at OpcLabs.EasyOpc.Implementations.Native.Assemblies.GetRawType(String name)
   at OpcLabs.EasyOpc.Implementations.Native.DataAccess.NativeEasyDAClient.get_RawType()
   at OpcLabs.EasyOpc.Implementations.Native.DataAccess.NativeEasyDAClient.set_AdaptableParameters(EasyDAAdaptableParameters value)
   at OpcLabs.EasyOpc.DataAccess.EasyDAClient..cctor()
   --- End of inner exception stack trace ---
   at OpcLabs.EasyOpc.DataAccess.EasyDAClient.Create()
   at QuickOpcPackageReference.Program.Main(String[] args) in C:\Users\binki\source\repos\QuickOpcPackageReference\QuickOpcPackageReference\Program.cs:line 9
```
