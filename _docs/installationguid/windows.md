---
title: Windows Guid
type: installguid
layout: single_markdown
position: 1
---

# Windows Guid
## Requirements

* [DownloadFamilies_2 Visual Studio 2017 Community](https://www.visualstudio.com/downloads/)
* [CMake](http://www.cmake.org/)
* [Git](http://git-scm.com/)
* [MySQL Server](http://dev.mysql.com/downloads/mysql/)

**Optional**
Microsoft Visual C++ 2017 Redistributable Package (Only if you run AscEmu on another PC as it was compiled)

**Helpful Programs**

*  Notepad++
*  HeidiSQL/SQLYog

# Getting the source

Use GitGui to get AscEmu source files.

## Download

**1.** Create a new folder, rightclick on it and choose GitGui

**2.** Choose "clone projectarchiv".

**3.** Fill in the required information:

* https://github.com/AscEmu/AscEmu
*  PathToYourFolder/NotExistingFolder

**4.** Click on "clone" and wait until everything is loaded.


# CMake Precompile

**1.** Open **CMake(cmake-gui)** and fill in the source-path and the build-path:

![cmake_1.JPG](/Wiki/images/cmake_1.JPG)

**2.** Choose your compiler (Visual Studio 12) or (Visual Studio 12 2013)

![cmake_2.JPG](/Wiki/images/cmake_2.JPG)

**3.** You should get a list with all available parts of our framework. Make your selection and press "Configure". Remember to create the folder specified under CMAKE_INSTALL_PREFIX, otherwise the INSTALL project will fail.

You can choose which client should be supported by AscEmu.

![cmake_3.JPG](/Wiki/images/cmake_3.JPG)

**4.** Now you can click on "Generate"

![cmake_4.JPG](/Wiki/images/cmake_4.JPG)

# VS Compiling

**1.** Open PathToYourPrecompiledSource/Ascemu.sln

**2.** Right-click on "Solution Ascemu" and choose "Build Solution" (F7).

![msvc_1.png](/Wiki/images/msvc_1.png)

**3.** Wait while VS compiles your binaries. At the end VS shows something like this:

![msvc_2.png](/Wiki/images/msvc_2.png)

**4.** Right-click on "INSTALL" and choose "Project Only -> Build Only INSTALL"

![msvc_3.png](/Wiki/images/msvc_3.png)

**5.** The required server files will now be in the folder specified by CMAKE_INSTALL_PREFIX (by default: C:\AscEmu)

# Database Setup

## Create the basic DBs

Create the 3 Databases.

```console
ascemu_logon  The login database (accounts)
ascemu_char   The characters database (All created characters)
ascemu_world  The world database (NPC, GO, Instances, Items, ...)
```

## Import the Structure

Import the structure for our databases. Use the files from ".../sql/xxx"

```console
character_structure -> ascemu_char DB
logon_structure -> ascemu_logon DB
```

For ascemu_world use the full_world from: http://www.board.ascemu.org/filebase/index.php/File/3-AscEmu-full-world-3-3-5/
{: .info }

## Updating the DBs

Make shure you use the updatefiles for the DBs. You can find them in ".../sql/"

```console
char_updates (all .sql files)  -> ascemu_char
logon_updates (all .sql files) -> ascemu_logon
world_updates (all .sql files) -> ascemu_world
```

**Done** Your databases are up to date. Move on with this guid.

# Extractors

You can find the extractors in:

```console
C:/Ascemu/tools/
```

Copy all extractors to you main WOW-folder (same folder where you can find wow.exe)

First run map_extractor.exe (output: dbc and maps)
Run vmaps.bat (output: vmaps)

**Optional**
You can test mmaps by running mmaps_generator (output: mmaps). This will take a long time...

Copy all output directories (dbc, maps, vmaps opt. mmaps) to your server folder (C:/Ascemu/)

# Configuration

Look for the *.conf files in the "configs" folder of AscEmu github-trunk. Copy the entire configs folder to your AscEmu Installation Folder in order for the server to read them.

Your "installation directory" should now look somewhat like this. 

```console
C:/Ascemu/configs/world.conf
C:/Ascemu/configs/logon.conf
```

## Configuring logon.conf

Enter your MySQL information at the the following section. 

```console
<LogonDatabase Hostname = "localhost"
Username = "ascemu"
Password = "ascemu"
Name     = "ascemu_logon"
Port     = "3306">
```

## Configuring world.conf

Enter your MySQL information at the the following section. 

```console
<WorldDatabase Hostname = "localhost" Username = "ascemu" Password = "ascemu" Name = "ascemu_world" Port = "3306">
<CharacterDatabase Hostname = "localhost" Username = "ascemu" Password = "ascemu" Name = "ascemu_char" Port = "3306">
```

The last step in configs/world.conf is to change line 502:

```console
RemotePassword = "change_me_world">
```

to:

```console
RemotePassword = "change_me_logon">
```

# Create an Account

**1.** Go to your world console and create an account.

```console
createaccount <accountname> <password>
```

example: createaccount admin adminpassword

**2.** Change permission(gmlevel) in your world console:

```console
setaccpermission <accountname> <permission>
```

example: setaccpermission admin az

**For further information about access levels, have a look to this page [GM_Access_Levels](http://www.ascemu.org/wiki/index.php?title=GM_Access_Levels "GM Access Levels")**
