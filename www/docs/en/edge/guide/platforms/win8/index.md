---
license: >
    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

title: Windows Platform Guide
---

# Windows Platform Guide

This guide shows how to set up your SDK development environment to build 
and deploy Cordova apps for Windows 8, Windows 8.1, Windows Phone 8.1, and 
Windows 10 Universal App Platform.  It shows how to use either shell tools 
to generate and build apps, or the cross-platform Cordova CLI discussed in 
[The Command-Line Interface](../../cli/index.html). (See the [Overview](../../overview/index.html) for a comparison of these 
development options.) This section also shows how to modify Cordova apps 
within Visual Studio. Regardless of which approach you take, you need to 
install the Visual Studio SDK, as described below.

See [Upgrading Windows 8](upgrade.html) for information on how to upgrade existing
Windows 8 Cordova projects.

Window Phone 8 (wp8) stays as a separate platform,
see [Windows Phone 8 Platform Guide](../wp8/index.html) for details.

Cordova WebViews running on Windows rely on Internet Explorer 10 (Windows 8.0)
and Internet Explorer 11 (Windows 8.1 and Windows Phone 8.1) as
their rendering engine, so as a practical matter you can use IE's
powerful debugger to test any web content that doesn't invoke Cordova
APIs.  The Windows Phone Developer Blog provides
[helpful guidance](http://blogs.windows.com/windows_phone/b/wpdev/archive/2012/11/15/adapting-your-webkit-optimized-site-for-internet-explorer-10.aspx)
on how to support IE along with comparable WebKit browsers.

## Requirements and Support

To develop apps for Windows platform you need:

- A Windows 8.1, 32 or 64-bit machine (_Home_, _Pro_, or _Enterprise_ editions) with minimum 4 GB of RAM.

- Windows 8.0, 8.1 or 10, 32 or 64-bit _Home_, _Pro_, or _Enterprise_
  editions, along with
  [Visual Studio 2012 Express](http://www.visualstudio.com/downloads) 
  or Visual Studio 2013.  Visual Studio 2015 is not able to build Windows 8.0 apps.

To develop apps for Windows 8.0 and 8.1 (including Windows Phone 8.1):

- Windows 8.1 or Windows 10, 32 or 64-bit _Home_, _Pro_, or _Enterprise_ editions,
  along with 
  [Visual Studio 2013 Express](http://www.visualstudio.com/downloads)
  or higher. An evaluation version of Windows 8.1 Enterprise is
  available from the
  [Microsoft Developer Network](http://msdn.microsoft.com/en-US/evalcenter/jj554510).

- For the Windows Phone emulators, Windows 8.1 (x64) Professional edition or higher,
and a processor that supports <a href='https://msdn.microsoft.com/en-us/library/windows/apps/ff626524(v=vs.105).aspx#hyperv'>Client Hyper-V and Second Level Address Translation (SLAT)</a>.
An evaluation version of Windows 8.1 Enterprise is available from the
[Microsoft Developer Network](http://msdn.microsoft.com/en-US/evalcenter/jj554510).

- [Visual Studio 2013 for Windows](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or higher).

To develop apps for Windows 10:

- Windows 8.1 or Windows 10 Technical Preview 2, 32- or 64-bit, along with
  [Visual Studio 2015 RC](http://www.visualstudio.com/preview) or higher.

App compatibility is determined by the OS that the app targeted.  Apps are forwardly-compatible
but not backwardly-compatible, so an app targeting Windows 8.1 cannot run on 8.0, but 
an app built for 8.0 can run on 8.1.

Follow the instructions at
[windowsstore.com](http://www.windowsstore.com/)
to submit the app to Windows Store.

To develop Cordova apps for Windows, you may use a PC running
Windows, but you may also develop on a Mac, either by running a
virtual machine environment or by using Boot Camp to dual-boot a
Windows 8.1 partition. Consult these resources to set up the required
Windows development environment on a Mac:

- [VMWare Fusion](http://msdn.microsoft.com/en-US/library/windows/apps/jj945426)

- [Parallels Desktop](http://msdn.microsoft.com/en-US/library/windows/apps/jj945424)
  
- [Boot Camp](http://msdn.microsoft.com/en-US/library/windows/apps/jj945423)
  
## Using Cordova Shell Tools

If you want to use Cordova's Windows-centered shell tools in
conjunction with the SDK, you have two basic options:

- Access them locally from project code generated by the CLI. They are
  available in the `platforms/windows/` directory after you add
  the `windows` platform as described below.

- Download them from a separate distribution at
  [cordova.apache.org](https://www.apache.org/dist/cordova/platforms/).
  The Cordova  distribution contains separate archives for each platform.
  Be sure to expand the appropriate archive, `cordova-windows` in
  this case, within an empty directory.  The relevant batch utilities
  are available in `package/bin` directory. (Consult the
  __README__ file if necessary for more detailed directions.)

These shell tools allow you to create, build, and run Windows apps.
For information on the additional command-line interface that enables
plugin features across all platforms, see Using Plugman to Manage
Plugins.

## Install the SDK

Install any edition of
[Visual Studio](http://www.visualstudio.com/downloads) matching the version
requirements listed above.  

![](img/guide/platforms/win8/win8_installSDK.png)

For Windows 10, the Visual Studio installer has an option to install tools to 
build Universal Windows Apps.  You must ensure that this option is selected
when installing to install the required SDK.

## Create a New Project

At this point, to create a new project you can choose between the
cross-platform CLI tool described in [The Command-Line Interface](../../cli/index.html), or
the set of Windows-specific shell tools. 
The CLI approach below generates an app named _HelloWorld_
within a new `hello` project directory:

        > cordova create hello com.example.hello HelloWorld
        > cd hello
        > cordova platform add windows

Here's the corresponding lower-level shell-tool approach:

        C:\path\to\cordova-windows\package\bin\create.bat C:\path\to\new\hello com.example.hello HelloWorld

This project targets Windows 8.1 as the default target OS.  You can choose to target 8.0 or 10.0 (see "Configure target Windows version" below) for all builds, or you target specific a particular version during each build.

## Build the Project

If you are using the CLI in development, the project directory's
top-level `www` directory contains the source files. Run either of
these within the project directory to rebuild the app:

        > cordova build
        > cordova build windows              # do not rebuild other platforms
        > cordova build windows   --debug    # generates debugging information
        > cordova build windows   --release  # signs the apps for release

Here's the corresponding lower-level shell-tool approach:

        C:\path\to\project\cordova\build.bat --debug        
        C:\path\to\project\cordova\build.bat --release

The `clean` command helps flush out directories in preparation for the
next `build`:

        C:\path\to\project\cordova\clean.bat 

## Configure target Windows version

By default `build` command produces two packages: Windows 8.0 and Windows Phone 8.1.
To upgrade Windows package to version 8.1 the following configuration setting must be 
added to configuration file (`config.xml`).

        <preference name="windows-target-version" value="8.1" />

Once you add this setting `build` command will start producing Windows 8.1 
and Windows Phone 8.1 packages.

### The --appx parameter

You may decide that you want to build a particular version of your application targeting a particular OS (for example, you might have set that you want to target Windows 10, but you want to build for Windows Phone 8.1).  To do this, you can use the `--appx` parameter:

        > cordova build windows -- --appx=8.1-phone

The build system will ignore the preference set in config.xml for the target Windows version and strictly build a package for Windows Phone 8.1.

Valid values for the `--appx` flag are `8.1-win`, `8.1-phone`, and `uap` (for Windows 10 Universal Apps).  These options also apply to the `cordova run` command.

### Considerations for target Windows version

Windows 10 supports a new "Remote" mode for Cordova apps (and HTML apps in general). This mode enables
apps much more freedom with respect to use of DOM manipulation and common web patterns such as the use 
of inline script, but does so by reducing the set of capabilities your app may use when 
submitted to the public Windows Store.  For more information about Windows 10 and Remote Mode, look at
the [Cordova for Windows 10](win10-support.md.html) documentation.

When using Remote Mode, developers are encouraged to apply a Content Security Policy (CSP) to their application 
to prevent script injection attacks.

## Deploy the app

To deploy Windows package:

        > cordova run windows -- --win  # explicitly specify Windows as deployment target
        > cordova run windows # `run` uses Windows package by default

To deploy Windows Phone package:

        > cordova run windows -- --phone  # deploy app to Windows Phone 8.1 emulator
        > cordova run windows --device -- --phone  # deploy app to connected device

You can use __cordova run windows --list__ to see all available targets and 
__cordova run windows --target=target_name -- --phone__ to run application on a 
specific device or emulator 
(for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

You can also use __cordova run --help__ to see additional build and run
options.

## Open the Project in the SDK and Deploy the App

Once you build a Cordova app as described above, you can open it with
Visual Studio. The various `build` commands generate a Visual Studio
Solution (_.sln_) file. Open the file in the File Explorer to modify
the project within Visual Studio:

![](img/guide/platforms/win8/win8_sdk_openSLN.png)

The `CordovaApp` component displays within the solution, and its `www`
directory contains the web-based source code, including the
`index.html` home page:

![](img/guide/platforms/win8/win8_sdk.png)

The controls below Visual Studio's main menu allow you to test or
deploy the app:

![](img/guide/platforms/win8/win8_sdk_deploy.png)

With __Local Machine__ selected, press the green arrow to install the
app on the same machine running Visual Studio. Once you do so, the app
appears in Windows 8's app listings:

![](img/guide/platforms/win8/win8_sdk_runApp.png)

Each time you rebuild the app, the version available in the interface
is refreshed.

Once available in the app listings, holding down the __CTRL__ key
while selecting the app allows you to pin it to the main screen:

![](img/guide/platforms/win8/win8_sdk_runHome.png)

Note that if you open the app within a virtual machine environment,
you may need to click in the corners or along the sides of the windows
to switch apps or access additional functionality:

![](img/guide/platforms/win8/win8_sdk_run.png)

Alternately, choose the __Simulator__ deployment option to view the
app as if it were running on a tablet device:

![](img/guide/platforms/win8/win8_sdk_sim.png)

Unlike desktop deployment, this option allows you to simulate the
tablet's orientation, location, and vary its network settings.

__NOTE__: Consult the [Overview](../../overview/index.html) for advice on how to use Cordova's
command-line tools or the SDK in your workflow. The Cordova CLI relies
on cross-platform source code that routinely overwrites the
platform-specific files used by the SDK. If you want to use the SDK to
modify the project, use the lower-level shell tools as an alternative
to the CLI.

## Supporting Toasts

Windows requires an app manifest capability declaration in order to support 
toast notifications.  When using the `cordova-plugin-local-notifications` 
plugin, or any other plugin that is attempting to use toast notifications,
add the following preference to your config.xml to enable it to publish 
toast notifications:

    <preference name="WindowsToastCapable" value="true" />

This preference sets the corresponding flag in your app manifest.  Plugins
should do the work necessary to configure the appearance of the 
displayed notifications.