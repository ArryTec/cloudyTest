# Microsoft Endpoint Configuration Manager Installation and Configuration:

Administrators use the Configuration Manager console to manage the Configuration Manager environment. Each Configuration Manager console can connect to a central administration site (CAS) or to a primary site. You can't connect a Configuration Manager console to a secondary site.

The Configuration Manager console is always installed on the site server for the CAS or a primary site. To install the console separate from site server installation, run the standalone installer.

# Prerequisites: 
Supported OS versions for Configuration Manager consoles

You have local Administrator rights on the target computer for the console.

You have Read permissions to the location of the console installation files.

.NET version requirements
Starting in version 2107, the console requires Microsoft .NET Framework version 4.6.2, but version 4.8 is recommended. If you install the console on other devices, make sure to update .NET. If the device doesn't already have it, the console setup doesn't install this prerequisite.

Starting in version 2103, the ConfigurationManager PowerShell module requires Microsoft .NET version 4.7.2 or later.

 Note

.NET Framework version 4.6.2 is preinstalled with Windows Server 2016 and Windows 10 version 1607. Later versions of Windows are preinstalled with a later version of the .NET Framework.

.NET Framework version 4.8 isn't supported on some OS versions, such as Windows 10 2015 LTSB.

For more information, see .NET Framework system requirements.

Source paths
Decide which source path to use:

ConsoleSetup folder in the installation path on the site server: \Tools\ConsoleSetup

When you install a site server, it copies the console installation files and supported language packs for the site to the Tools\ConsoleSetup subfolder. Optionally, you can copy the ConsoleSetup folder to an alternate location to start the installation. When you update the site, it always keeps its local version up to date.

Configuration Manager installation media: \SMSSETUP\BIN\I386

Installing the Configuration Manager console from the installation media always installs the English version. This behavior happens even if the site server supports different languages, or the target computer's OS is set to a different language.

When possible, start the console installer from the ConsoleSetup folder rather than from the source media.

 Important

Don't install the console using the CD.Latest source files. It's an unsupported scenario, and may cause problems with the console installation. For more information, see The CD.Latest folder.
If you create a package for installing the console on other computers, make sure the package includes the following files:
ConsoleSetup.exe
AdminConsole.msi
ConfigMgr.AC_Extension.i386.cab
ConfigMgr.AC_Extension.amd64.cab
Use the Setup Wizard
Browse to the source path, and open ConsoleSetup.exe.

 Important

Always install the console by using ConsoleSetup.exe. Although you can install the Configuration Manager console by running AdminConsole.msi, this method doesn't run prerequisites or dependency checks. The installation might not install correctly.

In the wizard, select Next.

On the Site Server page, enter the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console connects.

On the Installation Folder page, enter the installation folder for the Configuration Manager console. The folder path can't include trailing spaces or Unicode characters.

On the Ready to Install page, select Install.

Install from a command prompt
 Tip

Installing the Configuration Manager console from a command prompt always installs the English version. This behavior happens even if the target computer's OS is set to a different language. To install the Configuration Manager console in a language other than English, use the Setup Wizard.

ConsoleSetup.exe command-line options
/q
Installs the Configuration Manager console unattended. The TargetDir and DefaultSiteServerName options are required when you use this option.

/uninstall
Uninstalls the Configuration Manager console. Specify this option first when you use it with the /q option.

LangPackDir
Specifies the path to the folder that contains the language files. You can use Setup Downloader to download the language files. If you don't use this option, Setup looks for the language folder in the current folder. If the language folder isn't found, Setup continues to install English only. For more information, see Setup Downloader.

TargetDir
Specifies the installation folder to install the Configuration Manager console. This option is required when you use the /q option.

DefaultSiteServerName
Specifies the FQDN of the site server to which the console connects when it opens. This option is required when you use the /q option.

Examples
Silent install
ConsoleSetup.exe /q "TargetDir=%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com

Silent install with language packs
ConsoleSetup.exe /q "TargetDir=C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr

Silent uninstall
ConsoleSetup.exe /uninstall /q

Postinstallation information
The Configuration Manager console requires installation of the built-in WebView2 extension for certain features such as Community hub and dashboards. A notification to install the extension is given to the console user when they open the console. For more information see,the WebView2 console extension.

Next steps
An administrator sees objects in the console based on the permissions assigned to their user account. For more information, see Fundamentals of role-based administration.

For more information on the fundamentals of navigating the Configuration Manager console, see How to use the console.

If your environment uses a proxy server, this configuration may impact the functionality of the console. For more information, see Proxy server support - Configuration Manager console.
