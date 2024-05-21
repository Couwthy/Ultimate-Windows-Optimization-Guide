# Post-Install Instructions

# BIOS Configuration

- Enable XMP to improve RAM performance. Disabling unnecessary devices: Disable devices in the BIOS that you are not using to reduce system boot time. Then go into something like Avanced BIOS Features or OC/Overclocking settings or OC Tweaker and find the settings below and disable what I personally recommend (Hyper-Threading or SMT (AMD) , P-states/ C-states or (Global C-states Control, C1E, CPU C-states) , Intel(R) Speed Shift Technology).

## Choosing the Windows Version

- The choice between Windows 10 and Windows 11 should be based on several key factors, including technical requirements, functional preferences and specific user needs.

### Recommendations for Choosing the Windows Version:

- Windows 11: Recommended for Ryzen 7800x3d, 7900x3d, 7950x3d and Intel 12-14 generation processors with E-cores. Windows 11 offers improved support for the latest hardware and is optimized for modern gaming technologies such as Auto HDR and DirectStorage.
- Windows 10: Is the preferred choice for all other scenarios. Windows 10 continues to be a reliable and stable system for a wide range of hardware and gaming applications, providing high compatibility and performance.

# Actions After Installing the OS

### Installing Windows Updates

- Checking and Installing Updates: First of all, check for and install all available Windows updates to ensure the security and stability of the system.

## Install Drivers

- After installing the Windows 10 operating system, first install drivers from the motherboard website, excluding chipset and Intel ME, or use Snappy Driver Installer Origin. Then install the necessary software such as 7-Zip, office software, browsers, and other applications. Customize the power plans to match your platform. For AMD, download the driver from the official website and customize it, for Nvidia use NvCleanstall. Explain settings like Low Latency Mode and Pre-rendered frames to optimize system performance and responsiveness.

## Activate Windows

- Use the commands below to activate Windows using your license key if you do not have one linked to your HWID. Ensure that the activation process was successful by verifying the activation status in computer properties. Open CMD as administrator and enter the commands below.

```bat
slmgr /ipk <license key>
```

```bat
slmgr /ato
```



# Optimizing Windows Services

- This section discusses the standard service setup for Windows systems featuring the Desktop Experience, noting that while many Windows services are interdependent, some may be safely disabled if their features are not in use. It offers guidance in two parts: official Microsoft recommendations, then suggestions for alternative configurations. It emphasizes starting with Microsoft's advice, referencing specific support articles, before considering other changes, focusing on services Microsoft identifies as possibly disableable without affecting the user experience.

## System Services Summary

- This is a list of services which Microsoft has recommendations for disabling, if a service is not on this list then Microsoft is unsure of the impacts it may have on the desktop experience.

| Service | Service Name | Impacts | My Recommendation
| --- | --- | --- | --- |
| AxInstSV | ActiveX Installer | Provides User Account Control validation for the installation of ActiveX controls from the Internet and enables management of ActiveX control installation based on Group Policy settings | Disable |
| tzautoupdate | Auto Time Zone Updater | Automatically sets the system time zone. | Keep Disabled |
| bthserv | Bluetooth Support Service | The Bluetooth service supports discovery and association of remote Bluetooth devices. Stopping or disabling this service may cause already installed Bluetooth devices to fail to operate properly and prevent new devices from being discovered or associated. | Disable if you don't use or plan to use Bluetooth devices |
| CDPUserSvc | Connected Devices Platform Service | If you deactivate it, the automatic mail retrieval, the update of the LiveTiles and the Infocenter should be dead. In addition, OndeDrive will no longer sync and a number of other synchronization-dependent features will cease the service. | See per-user services section |
| PimIndexMaintenanceSvc | ContactData | Indexes contact data for fast contact searching. If you stop or disable this service, contacts might be missing from your search results. | Disable completely or Per-User for shared computers, see Per-User services section. |
| dmwappushservice  | Device Management Wireless Application | Service required on client devices for Intune, MDM and similar management technologies, and for Unified Write Filter. Not needed for Server. | Disable, for mobile |
| MapsBroker | Downloaded Maps Manager | Windows service for application access to downloaded maps. This service is started on-demand by application accessing downloaded maps. Disabling this service will prevent apps from accessing maps. | Disable if you don't use any apps that use Map based features. |
| lfsvc | Geolocation Service | This service monitors the current location of the system and manages geofences (a geographical location with associated events). If you turn off this service, applications will be unable to use or receive notifications for geolocation or geofences. | Disable |
| SharedAccess | Internet Connection Sharing | Provides network address translation, addressing, name resolution and/or intrusion prevention services for a home or small office network. | Disable |
| lltdsvc | Link-Layer Topology Discovery Mapper | Creates a Network Map, consisting of PC and device topology (connectivity) information, and metadata describing each PC and device. If this service is disabled, the Network Map will not function properly. | Disable |
| wlidsvc | Microsoft Account Sign-in Assistant | Enables user sign-in through Microsoft account identity services. If this service is stopped, users will not be able to log on to the computer with their Microsoft account. | Disable if you don't use a Microsoft account to sign-in, or for the Microsoft Store |
| AppVClient | Microsoft App-V Client | Manages App-V users and virtual applications | Disable |
| NgcSvc | Microsoft Passport | Provides process isolation for cryptographic keys used to authenticate to a user's associated identity providers. If this service is disabled, all uses and management of these keys will not be available, which includes machine logon and single-sign on for apps and websites. | Leave Enabled |
| NgcCtnrSvc | Microsoft Passport Container | Manages local user identity keys used to authenticate user to identity providers as well as TPM virtual smart cards. If this service is disabled, local user identity keys and TPM virtual smart cards will not be accessible. | Leave Enabled |
| NetTcpPortSharing | Net.Tcp Port Sharing Service | Provides ability to share TCP ports over the net.tcp protocol. | Keep Disabled |
| NcbService | Network Connection Broker | Brokers connections that allow Microsoft Store Apps to receive notifications from the internet. | Leave enabled unless you disable all CDP services (system and user), dependency |
| CscService | Offline Files | The Offline Files service performs maintenance activities on the Offline Files cache, responds to user logon and logoff events | Keep Disabled |
| PhoneSvc | Phone Service | Manages the telephony state on the device | Disable |
| Spooler | Print Spooler | This service spools print jobs and handles interaction with the printer. If you turn off this service, you won't be able to print or see your printers. | Disable unless you use printers or scanners |
| PrintNotify | Printer Extensions and Notifications | This service opens custom printer dialog boxes and handles notifications from a remote print server or a printer. | Disable, unless you use printers or scanners |
| PcaSvc | Program Compatibility Assistant Service | This service provides support for the Program Compatibility Assistant (PCA). PCA monitors programs installed and run by the user and detects known compatibility problems. | Pending |
| QWAVE | Quality Windows Audio Video Experience | Quality Windows Audio Video Experience (qWave) is a networking platform for Audio Video (AV) streaming applications on IP home networks. | Disable |
| RmSvc | Radio Management Service | Radio Management and Airplane Mode Service | Disable if you don't use or plan to use wifi etc |
| RemoteAccess | Routing and Remote Access | Offers routing services to businesses in local area and wide area network environments. | Disable |
| SensorDataService | Sensor Data Service | Delivers data from a variety of sensors | Disable |
| SensrSvc | Sensor Monitoring Service | Monitors various sensors in order to expose data and adapt to system and user state. If this service is stopped or disabled, the display brightness will not adapt to lighting conditions. | Disable |
| SensorService | Sensor Service | A service for sensors that manages different sensors' functionality. | Disable |
| ShellHWDetection | Shell Hardware Detection | Provides notifications for AutoPlay hardware events. | Disable |
| SCardSvr | Smart Card | Manages access to smart cards read by this computer. | Disable if you don't use smart cards |
| ScDeviceEnum | Smart Card Device Enumeration Service | Creates software device nodes for all smart card readers accessible to a given session. | Disable if you don't use smart cards |
| SSDPSRV | SSDP Discovery | Discovers networked devices and services that use the SSDP discovery protocol, such as UPnP devices. | Disable |
| WiaRpc | Still Image Acquisition Events | Launches applications associated with still image acquisition events. | Disable if you don't use a scanner. |
| OneSyncSvc | Sync Host | This service synchronizes mail, contacts, calendar and various other user data. | Disable completely or Per-User for shared computers, see Per-User services section. |
| TabletInputService | Touch Keyboard and Handwriting Panel Service | Enables Touch Keyboard and Handwriting Panel pen and ink functionality | Disable if you don't use these features. |
| upnphost | UPnP Device Host | Allows UPnP devices to be hosted on this computer. If this service is stopped, any hosted UPnP devices will stop functioning and no additional hosted devices can be added. | Disable |
| UserDataSvc | User Data Access | Provides apps access to structured user data, including contact info, calendars, messages, and other content. | Disable if you don't use these built-in features |
| UevAgentService | User Experience Virtualization Service | Provides support for application and OS settings roaming | Keep disabled |
| WalletService | WalletService | Hosts objects used by clients of the wallet | Disable |
| FrameServer | Windows Camera Frame Server | Enables multiple clients to access video frames from camera devices. | Disable |
| stisvc | Windows Image Acquisition | Provides image acquisition services for scanners and cameras | Disable if you don't use image scanners |
| wisvc | Windows Insider Service | Windows Insider Service | Disable if you don't subscribe to insider services |
| icssvc | Windows Mobile Hotspot Service | Provides the ability to share a cellular data connection with another device. | Disable |
| WpnService | Windows Push Notifications System Service | This service runs in session 0 and hosts the notification platform and connection provider which handles the connection between the device and WNS server. | Leave Enabled |
| WpnUserService | Windows Push Notifications User Service | This service hosts Windows notification platform which provides support for local and push notifications. Supported notifications are tile, toast and raw. | Leave Enabled, see per-user services |
| WSearch | Windows Search | Provides content indexing, property caching, and search results for files, e-mail, and other content. | Disable |
| XblAuthManager | Xbox Live Auth Manager | Provides authentication and authorization services for interacting with Xbox Live. If this service is stopped, some applications may not operate correctly. | Disable if you don't use XBox Live Features |
| XblGameSave | Xbox Live Game Save | This service syncs save data for Xbox Live save enabled games. If this service is stopped, game save data will not upload to or download from Xbox Live. | Disable if you don't use XBox Live Features |


- To disable the specified services while excluding those under review and essential per-user services, copy the provided command into an administrative PowerShell terminal. After executing the command, restart your computer to apply the changes.

    ```
    Set-Service AxInstSV -StartupType Disabled
    Set-Service tzautoupdate -StartupType Disabled
    Set-Service bthserv -StartupType Disabled
    Set-Service dmwappushservice -StartupType Disabled
    Set-Service MapsBroker -StartupType Disabled
    Set-Service lfsvc -StartupType Disabled
    Set-Service SharedAccess -StartupType Disabled
    Set-Service lltdsvc -StartupType Disabled
    Set-Service AppVClient -StartupType Disabled
    Set-Service NetTcpPortSharing -StartupType Disabled
    Set-Service CscService -StartupType Disabled
    Set-Service PhoneSvc -StartupType Disabled
    Set-Service Spooler -StartupType Disabled
    Set-Service PrintNotify -StartupType Disabled
    Set-Service QWAVE -StartupType Disabled
    Set-Service RmSvc -StartupType Disabled
    Set-Service RemoteAccess -StartupType Disabled
    Set-Service SensorDataService -StartupType Disabled
    Set-Service SensrSvc -StartupType Disabled
    Set-Service SensorService -StartupType Disabled
    Set-Service ShellHWDetection -StartupType Disabled
    Set-Service SCardSvr -StartupType Disabled
    Set-Service ScDeviceEnum -StartupType Disabled
    Set-Service SSDPSRV -StartupType Disabled
    Set-Service WiaRpc -StartupType Disabled
    Set-Service TabletInputService -StartupType Disabled
    Set-Service upnphost -StartupType Disabled
    Set-Service UserDataSvc -StartupType Disabled
    Set-Service UevAgentService -StartupType Disabled
    Set-Service WalletService -StartupType Disabled
    Set-Service FrameServer -StartupType Disabled
    Set-Service stisvc -StartupType Disabled
    Set-Service wisvc -StartupType Disabled
    Set-Service icssvc -StartupType Disabled
    Set-Service WSearch -StartupType Disabled
    Set-Service XblAuthManager -StartupType Disabled
    Set-Service XblGameSave -StartupType Disabled
    ```
- This section highlights per-user services not included in the PowerShell command summary, such as CDPUserSvc and OneSyncSvc, among others. Microsoft suggests configurations for these services, which are designed to start upon user login and are unique to each user session. For instance, the ContactData service will appear as ContactData_37664 for a specific user, indicating a per-user instance. Disabling these services prevents them from launching automatically with each user session.


| Service | Service Name | Impacts | My Recommendation
| --- | --- | --- | --- |
| BcastDVRUserService | GameDVR and Broadcast User Service | Used for Game Recordings and Live Broadcasts | Disable if not using these features |
| BluetoothUserService | Bluetooth User Support Service | The Bluetooth service supports discovery and association of remote Bluetooth devices. Stopping or disabling this service may cause already installed Bluetooth devices to fail to operate properly and prevent new devices from being discovered or associated. | Disable if you don't use or plan to use Bluetooth devices |
| PimIndexMaintenanceSvc | Contact Data | Indexes contact data for fast contact searching. If you stop or disable this service, contacts might be missing from your search results. | Disable, if you don't use Contacts app data.
| CaptureService | Capture Service | Related to Speech capture services, may impact web camera or other voice input | Leave Enabled
| DevicePickerUserSvc | Device Picker | Unknown | Leave Enabled
| DevicesFlowUserSvc | Devices Flow | Unknown | Leave Enabled
| MessagingService | MessagingService | Service supporting text messaging and related functionality | Disable
| CDPUserSvc | CDPUserSvc | This service is used for Connected Devices and Universal Glass scenarios | Leave Enabled, may have negative impact on user experience
| OneSyncSvc | Sync Host | Synchronizes mail, contacts, calendar, and other user data. Mail and other applications dependent on this service don't work correctly when this service is not running. | Leave Enabled, may have negative impact on user experience
| UserDataSvc | User Data Access | Provides apps access to structured user data, including contact info, calendars, and messages. If you stop or disable this service, apps that use this data might not work correctly. | Leave Enabled, may have negative impact on user experience
| UnistoreSvc| User Data Storage | Handles storage of structured user data, including contact info, calendars, and messages. If you stop or disable this service, apps that use this data might not work correctly. | Leave Enabled, may have negative impact on user experience
| WpnUserService | Windows Push Notifications User Service | Hosts Windows notification platform, which provides support for local and push notifications. Supported notifications are tile, toast, and raw. | Leave Enabled, may have negative impact on user experience
| PrintWorkflowUserSvc | PrintWorkflow | Print Workflow | Leave Enabled

## Alternative Service Configuration Overview

## Alternative Services Summary

| Service | Service Name | Impacts | My Recommendation
| --- | --- | --- | --- |
| SEMgrSvc | Payments and NFC/SE Manager | Near field communications for payments, tap to pay | Disable |
| DiagTrack | Connected User Experiences and Telemetry |  The Connected User Experiences and Telemetry service enables features that support in-application and connected user experiences. Additionally, this service manages the event-driven collection and transmission of diagnostic and usage information (used to improve the experience and quality of the Windows Platform) when the diagnostics and usage privacy option settings are enabled under Feedback and Diagnostics. | Disable

- Use the following to disable all those noted above **except** those pending review.
  - Paste the following into an administrative Powershell terminal, press enter, the restart your computer for it to take effect.

    ```
    Set-Service SEMgrSvc -StartupType Disabled
    Set-Service DiagTrack -StartupType Disabled
    ```


#### GPU and DirectX Graphics Kernel

- [AutoGpuAffinity](https://github.com/amitxv/AutoGpuAffinity) can be used to benchmark the most performant CPUs that the GPU-related modules are assigned to.

#### XHCI and Audio Controller

- The XHCI and audio controller related modules generate a substantial amount of interrupts upon interaction respective of the relevant device. Isolating the related modules to an underutilized CPU is beneficial for reducing contention.

# Device Manager


- Access Device Manager (devmgmt.msc) and deactivate any hardware components or drivers that are not currently in use. Exercise caution to avoid disabling anything essential. It's worth noting that uninstalling drivers via Device Manager may lead to their automatic reinstallation upon reboot. To fully prevent a driver from functioning, it's better to disable it rather than uninstalling it. Disabling a device or driver in Device Manager unloads it, preventing it from interrupting the CPU and potentially causing system slowdowns or interruptions due to poorly programmed drivers.

### What to disable:
```
Intel graphics (if you don’t use it, ideally should be disabled in the BIOS)
Microsoft ISATAP Adapter
Microsoft iSCSI Initiator
Composite Bus Enumerator
Intel Management Engine / AMD PSP
Intel SPI (flash) Controller
Microsoft GS Wavetable Synth
Microsoft Virtual Drive Enumerator (if not using virtual drives)
NDIS Virtual Network Adapter Enumerator
Remote Desktop Device Redirector Bus
SMBus
System speaker
Terminal Server Mouse/Keyboard drivers
UMBus
``` 

# Debloat

- Uninstalling unnecessary pre-installed applications and services, is a process that some users perform to optimize system performance and reduce its overall size. However, this process should be approached with caution because removing some components can affect the stability and functionality of the operating system. Make sure you understand the potential risks and back up important data before proceeding with this operation.
```
Powershell -command "Get-AppxPackage -allusers Microsoft.Wallet | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsAlarms | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsCalculator | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsCamera | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsFeedbackHub | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Disney.37853FC22B2CE | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.549981C3F5F10 | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.BingNews | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.BingWeather | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.GetHelp | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.Getstarted | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.Microsoft3DViewer | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.MicrosoftOfficeHub | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.MicrosoftSolitaireCollection | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.MicrosoftStickyNotes | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.MixedReality.Portal | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.MSPaint | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.Office.OneNote | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.OneDriveSync | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.People | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.PowerAutomateDesktop | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.ScreenSketch | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.SkypeApp | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.Todos | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsMaps | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.WindowsSoundRecorder | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.YourPhone | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.ZuneMusic | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers Microsoft.ZuneVideo | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers MicrosoftTeams | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers MicrosoftWindows.Client.WebExperience | Remove-AppxPackage"
Powershell -command "Get-AppxPackage *Microsoft.WebpImageExtension* | Remove-AppxPackage"
Powershell -command "Get-AppxPackage *Microsoft.WebMediaExtensions* | Remove-AppxPackage"
Powershell -command "Get-AppxPackage *Microsoft.Print3D* | Remove-AppxPackage"
Powershell -command "Get-AppxPackage *Microsoft.HEIFImageExtension* | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers SpotifyAB.SpotifyMusic | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers microsoft.windowscommunicationsapps | Remove-AppxPackage"
Powershell -command "Get-AppxPackage -allusers yandex | Remove-AppxPackage"
Powershell -command "Get-AppxPackage *Microsoft.549981C3F5F10* | Remove-AppxPackage"
Powershell -command "Get-WindowsPackage -Online | Where PackageName -like *Hello-Face* | Remove-WindowsPackage -Online -NoRestart"
Powershell -command "Get-WindowsPackage -Online | Where PackageName -like *QuickAssist* | Remove-WindowsPackage -Online -NoRestart"
%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall
rd "%LocalAppData%\Microsoft\OneDrive" /Q /S
rd "%ProgramData%\Microsoft OneDrive" /Q /S
rd "C:\OneDriveTemp" /Q /S
REG Delete "HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /f
REG Delete "HKEY_CLASSES_ROOT\Wow6432Node\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}" /f
```

## Customizing Optimal Registry Settings

- Customizing optimal registry settings and cleaning up your Windows system through the registry editor can improve the performance and stability of your operating system. However, you need to be careful when making changes to the registry, as incorrect settings can lead to undesirable consequences. It is recommended to create a restore point before making changes.

```
Windows Registry Editor Version 5.00

;Automatic Mainenance Disable
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\Maintenance]
"MaintenanceDisabled"=dword:00000001

;Disable Mouse Keys
[HKEY_CURRENT_USER\Control Panel\Accessibility\MouseKeys]
"Flags"="0"

;Disable Sticky Keys
[HKEY_CURRENT_USER\Control Panel\Accessibility\StickyKeys]
"Flags"="0"

;Disable Keyboard Response
[HKEY_CURRENT_USER\Control Panel\Accessibility\Keyboard Response]
"Flags"="0"

;Disabel Toggle Keys
[HKEY_CURRENT_USER\Control Panel\Accessibility\ToggleKeys]
"Flags"="0"

;Network Settings
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile]
"NetworkThrottlingIndex"=dword:0000000a
"SystemResponsiveness"=dword:0000000a

;Disable UAC
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System]
"EnableVirtualization"=dword:00000000
"EnableInstallerDetection"=dword:00000000
"PromptOnSecureDesktop"=dword:00000000
"EnableLUA"=dword:00000000
"EnableSecureUIAPaths"=dword:00000000
"ConsentPromptBehaviorAdmin"=dword:00000000
"ValidateAdminCodeSignatures"=dword:00000000
"EnableUIADesktopToggle"=dword:00000000
"ConsentPromptBehaviorUser"=dword:00000000
"FilterAdministratorToken"=dword:00000000


;Allow users to enable online speech recognition services
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\InputPersonalization]
"AllowInputPersonalization"=dword:00000000

;Turn off automatic learning
[HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\InputPersonalization]
"RestrictImplicitInkCollection"=dword:00000001
"RestrictImplicitTextCollection"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\InputPersonalization]
"RestrictImplicitInkCollection"=dword:00000001
"RestrictImplicitTextCollection"=dword:00000001

;Getting to know you
[HKEY_CURRENT_USER\Software\Microsoft\InputPersonalization]
"RestrictImplicitInkCollection"=dword:00000001
"RestrictImplicitTextCollection"=dword:00000001

[HKEY_CURRENT_USER\Software\Microsoft\InputPersonalization\TrainedDataStore]
"HarvestContacts"=dword:00000000

[HKEY_CURRENT_USER\Software\Microsoft\Personalization\Settings]
"AcceptedPrivacyPolicy"=dword:00000000

[HKEY_CURRENT_USER\Control Panel\Desktop]
"CursorBlinkRate"="-1"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\NetBT]
"Start"=dword:00000004

[HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\PriorityControl]
"Win32PrioritySeparation"=dword:00000002

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\NDIS\Parameters]
"TrackNblOwner"=dword:00000000
```

# Disabling Mouse Acceleration

- Mouse acceleration can significantly affect accuracy in games, especially in genres where precise movements are important, such as first-person shooters. Disabling mouse acceleration provides more predictable and accurate cursor control.

 ```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Control Panel\Mouse]
"MouseSpeed"="0"
"MouseThreshold1"="0"
"MouseThreshold2"="0"
 ```


### Disable Idle States

```bat
powercfg /setacvalueindex scheme_current sub_processor 5d76a2ca-e8c0-402f-a133-2158492d58ad 1 && powercfg /setactive scheme_current
```

### Enable Idle States (default)

```bat
powercfg /setacvalueindex scheme_current sub_processor 5d76a2ca-e8c0-402f-a133-2158492d58ad 0 && powercfg /setactive scheme_current
```

## Cleanup

- Configure Disk Cleanup

```
del /s /f /q c:\windows\temp\*.*
rd /s /q c:\windows\temp
md c:\windows\temp
del /s /f /q C:\WINDOWS\Prefetch
del /s /f /q %temp%\*.*
rd /s /q %temp%
md %temp%
```
