# ARViz

Intelligent Robotics http://intelligentrobotics.es/ @IntellRobotLabs 

ARViz is an RViz implementation for Augmented Reality. This application runs inside the Microsoft Hololens AR device as a UWP application, without the need to use Ros Bridge. This project has as goal to combine:

* ROS2 C # support for UWP applications on board Microsoft Hololens.
* TF2 support for ROS C#.
* Secure communications.
* Hololens Positioning in the scene.

This project uses the [UWP port of ROS2](https://github.com/esteve/ros2_dotnet) done by [Esteve Fernández](https://github.com/esteve). You can have a look at the talk he gave at ROSCon 2018 about ROS2 for Android, iOS and UWP to understand the underlying code [Video](https://vimeo.com/293302046) [Slides](https://roscon.ros.org/2018/presentations/ROSCon2018_ROS2%20for%20Android,%20iOS%20and%20Universal%20Windows%20Platform.pdf).

This project is funded by [ROSIN](http://rosin-project.eu/) as a focused Technical Project.

Project mantainers:
* David Vargas (dvargas@inrobots.es)
* Francisco Martín (fmrico@gmail.com)

Advisor:
* Esteve Fernández (esteve@apache.org)

## Building ROS2 for UWP

Follow the instructions on [ros2-dotnet](https://github.com/esteve/ros2_dotnet) to compile [ROS2 for UWP](https://github.com/esteve/ros2_dotnet/blob/master/README.md#universal-windows-platform-arm-win32-win64)

## Using generated DLLs in your UWP application from Visual Studio

Create a new Visual Studio project (Visual C# - Windows Universal - Empty app).

In Solution Explorer panel: 
```
right click on Universal Windows project - Add - Existing item... 
```
and include every DLL file from `{your_ros2_uwp_ws}\install\bin`. Now select all of these files in Solution Explorer and check/set the properties:
```
Build action: Content
Copy to output directory: Copy always
```
This allows you to retrieve the files in the same directory as the assembly.

Nest step, in Solution Explorer panel:
```
right click on References - Add reference... 
```
and include `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_assemblies.dll`, `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_common.dll` and `{your_ros2_uwp_ws}\install\lib\std_msgs\dotnet\std_msgs_assemblies.dll`.

Now you can include your ROS2 code in MainPage.xaml.cs script, compile your project and run it on HoloLens Emulator or HoloLens physical device.

## Using generated DLLs in your UWP application from Unity
**NOTE: _Tested on `Unity 2018.2.8f1`_**

Create a new Unity project and set up the following editor properties.

### Build Settings
Set your target platform properly:
```
File - Build Settings - Universal Windows Platform - Switch Platform
```
then set UWP build settings:
```
Target Device: HoloLens
Build Type: D3D
SDK: Latest installed
Visual Studio Version: Latest installed
Build and Run on: Local Machine and Windows Phone
Build Configuration: Release
```
and let unchecked the rest.

### Player Settings

- Other Settings

  **Configuration**
  ```
  Scripting Runtime Version: .NET 4.x Equivalent
  Scripting Backend: .NET
  Api Compatibility Level: .NET 4.x
  ```
 
- Publishing Settings

  **Capabilities**
  - [x] InternetClient
  - [x] InternetClientServer
  - [x] PrivateNetworkClientServer
 
- XR Settings
  - [x] Virtual Reality Supported
  
  Virtual Reality SDKs
    > Windows Mixed Reality

### Add files
Create Assets/Plugins and Assets/Scripts folders. 

In Plugins folder include every DLL file from `{your_ros2_uwp_ws}\install\bin`. Also include `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_assemblies.dll`, `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_common.dll` and `{your_ros2_uwp_ws}\install\lib\std_msgs\dotnet\std_msgs_assemblies.dll`.

In Scripts folder create your C# scripts and attach them to a scene GameObject to execute them when the app starts.

Finally, build your project to generate a Visual Studio solution.
```
File - Build Settings - Build
``` 

### Unity generated Visual Studio solution
Open the VS solution generated after building your Unity project.
In Solution Explorer panel: 
```
right click on Universal Windows project - Add - Existing item... 
```
and include every DLL file from `{your_ros2_uwp_ws}\install\bin`. Now select all of these files in Solution Explorer and check/set the properties:
```
Build action: Content
Copy to output directory: Copy always
```
This allows you to retrieve the files in the same directory as the assembly.

Nest step, in Solution Explorer panel:
```
right click on References - Add reference... 
```
and include `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_assemblies.dll`, `{your_ros2_uwp_ws}\install\lib\rcldotnet\dotnet\rcldotnet_common.dll` and `{your_ros2_uwp_ws}\install\lib\std_msgs\dotnet\std_msgs_assemblies.dll`.

Finally compile your project and run it on HoloLens Emulator or HoloLens physical device.
