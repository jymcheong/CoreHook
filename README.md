# CoreHook

A library to hook unmanaged applications by hosting .NET Core and running managed code to extend an application's functionality (more information [here](https://github.com/dotnet/docs/blob/master/docs/core/tutorials/netcore-hosting.md)) on various architectures running  [Linux](https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore2x), [macOS](https://docs.microsoft.com/en-us/dotnet/core/macos-prerequisites?tabs=netcore2x), and [Windows](https://docs.microsoft.com/en-us/dotnet/core/windows-prerequisites?tabs=netcore2x).  

Inspired and based on the great [EasyHook](https://github.com/EasyHook/EasyHook).

## Dependencies

* [.NET Core](https://docs.microsoft.com/en-us/dotnet/core/)
* [CoreHook.Hooking](https://github.com/unknownv2/CoreHook.Hooking)
* [CoreHook.Host](https://github.com/unknownv2/CoreHook.Host)
* [CoreHook.ProcessInjection](https://github.com/unknownv2/CoreHook.ProcessInjection)
* [CoreHook.UnixHook](https://github.com/unknownv2/CoreHook.UnixHook)
* [JsonRpc (For Examples Only)](https://github.com/CXuesong/JsonRpc.Standard) 


## Supported Platforms

| Architecture  | Operating System      | Working    |
| ------------- |:---------------------:|:----------:|
| x86           | Windows               | Yes        |
| x64           | Linux, macOS, Windows | Yes        |
| ARM32         | Linux, Windows        | Windows    |
| ARM64         | Linux, Windows        | WIP        |

## Tested Platforms

| Operating System    | Architecture(s)       |
| ------------------  |:---------------------:|
| macOS High Sierra   | x64                   |
| Ubuntu 14           | x64                   |
| Ubuntu 16           | x64                   |
| Windows 7 SP1       | x86, x64              |
| Windows 8.1         | x86, x64              |
| Windows 10 (Win32)  | x86, x64, ARM32       |
| Windows 10 (UWP)    | x86, x64              |
| Windows Server 2008 | x86, x64              |
| Windows Server 2012 | x86, x64              |
| Windows Server 2016 | x86, x64              |

## Examples

 * [FileMonitor - Linux and macOS (Unix)](Examples/Unix/CoreHook.Unix.FileMonitor/)
 * [FileMonitor - Universal Windows Platform (UWP)](Examples/UWP/CoreHook.UWP.FileMonitor/) 
 * [FileMonitor - Windows Desktop Applications (Win32)](Examples/CoreHook.FileMonitor)

## Notes on UWP Usage

 There are two UWP sample programs included in the Examples folder: CoreHook.UWP.FileMonitor and CoreHook.UWP.FileMonitor2. 
 
 The problem is that there is currently no way to set the proper access control on our pipes on the .NET Core platform and the issue is [being tracked here](https://github.com/dotnet/corefx/issues/30170).

 `CoreHook.UWP.FileMonitor` targets .NET Framework version 4.6.1 to support setting permissions on the NamedPipeServerStreams we create for communication with the target process since our libraries target .NET Standard 2.0 ([more information here](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)).

 `CoreHook.UWP.FileMonitor2` targets .NET Core 2.1 and uses CoreHook to hook the `kernel32.dll!CreateNamedPipeW` function and in our callback, we set the proper permisions and return the handle for use in our NamedPipeServerStream constructor. Using this method, we can also choose which pipes to modify since we have access to their names as the first argument of the function. 

**The library is still in development and a lot might be broken. Pull requests/contributions are all welcome!**