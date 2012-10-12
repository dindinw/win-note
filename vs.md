Free VC Compiler
-----------------
  see also http://en.wikipedia.org/wiki/Microsoft_Visual_Studio

  * VC71 (Visual Studio 2003 tookit)   
    1. deleted 
    2. 90d8b963ca196aa9855b2ca6c3174c14  VCToolkitSetup.exe  (unverified)

  * VC8  (Visual Studio 2005 express)   
    deleted

  * VC9  (Visual Studio 2008 Express Editions with SP1)
    1. http://www.microsoft.com/downloads/details.aspx?FamilyId=F3FBB04E-92C2-4701-B4BA-92E26E408569&displaylang=en
    2. download windows 7 SDK

  * VC10 (Visual Studio 2010 Expres)    
    1. http://go.microsoft.com/?linkid=9709949
    2. download windows 7 SDK

  * VC11 (Visual Studio 2012 Express for Windows Desktop) download ISO
    1. 
    2012_WDX_ENU.iso 19c0dfe95e688a2b3da63dfae0c68475
    2. Windows 8 SDK?

Windows SDK
-----------
  see also http://en.wikipedia.org/wiki/Microsoft_Windows_SDK

  * 8.0a 
    Windows Software Development Kit (SDK) for Windows 8

  * 7.1 SDK
    http://www.microsoft.com/en-us/download/details.aspx?id=8442
    Microsoft Windows SDK for Windows 7 and .NET Framework 4 (ISO)
    Version:	7.1	Date published:	5/19/2010
    x86 ISO File Name: GRMSDK_EN_DVD.iso 
    CRC#: 0xBD8F1237 
    SHA1: 0xCDE254E83677C34C8FD509D6B733C32002FE3572 
    
    a7a4aa8a9f5b648f5771eafe2286817f  GRMSDK_EN_DVD.iso

  * 7.0 SDK (web download only?) 
    Microsoft Windows SDK for Windows 7 and .NET Framework 3.5 SP1
    Version:	7	Date published:	7/24/2009
    (need VS2008 sp1)

  * 7.0A
    included in Visual Studio 2010  

  * 6.1 (don't use it)   
    Windows SDK for Windows Server 2008 and .NET Framework 3.5
    Version:	6.1	Date published:	2/5/2008

DirectX
-------
  * DirectX 9.0 Complete Software Development Kit (SDK)
    Version:	9.0	Date published:	8/27/2012
    dx9sdk.exe	222.4 MB

  * DirectX 9.0b Software Development Kit (SDK) for C/C++
    Version:	9.0	Date published:	8/27/2012
    dx9sdkcp.exe	97.7 MB



VS INSTALLATION
===============

WIN8 RP + VS2012 Express RTM
----------------------------
Gernally, It impossiable, since Windows8 RP only works with VS2012 RC (WIN8 RTM works with VS2012 RTM) but RC is not available now.
We need to do some dirty modification. let it work. 

### Download VS2012 Express for windows 8 RTM
  
  * Note: you need to download 'for windows 8' not for 'windows desktop'
### Active administrator  
  1. run 'cmd' as administrator
  2. exectue `net user administrator /active:yes`
  3. login out/in as administrator 
### Change registry
  1. run 'regedit'
  2. go to `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\NET Framework Setup\NDP\v4\Full`
  3. right click->'Pemission"->"Advanced"->"Owener" change to administrator
  4. change Version to '4.5.50709'
### Installation
  normal installation, done!

