# Configure the NVIDIA Driver

- If you do not need the GeForce Experience, follow these steps, run the driver installer and go straight to the video driver setup. If you don't need it, unzip the driver with your archiver into a folder. Delete all files from the folder, leaving only the necessary files.

```
Display.Driver
NVI2
EULA.txt
ListDevices.txt
setup.cfg
setup.exe
 ```
- Open the setup.cfg file with notepad and delete the following three lines:

 ```
<file name="${{EulaHtmlFile}}"/>
<file name="${{FunctionalConsentFile}}"/>
<file name="${{PrivacyPolicyFile}}"/>
 ```

- Open CMD and enter the command below to disable telemetry

    ```bat
    reg add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\Startup\SendTelemetryData" /t REG_DWORD /d "0" /f
    ```

- Run the setup.exe file and install the driver.

### Setting MSI Afterburner

- In MSI Afterburner program you need to turn off limits or increase them to maximum and turn on stable voltages, voltage monitoring and remember the video card model. After in the browser find the passport frequency boost and memorize it. 

- In the program MSI Afterburner enable key boost, for which you need to put the skin [EVGA SKIN](https://drive.google.com/file/d/1buaP5Gv7f3Jv3OPQzKWF6Q7fSvxft2a0/view?usp=sharing). To do this, download the archive with the skins folder and copy the default file to the skins folder. After rebooting the computer, select the skin and enable keyboost.

### Setting up the video driver

- If you need the NVIDIA control panel to customize 3D settings, you may be missing data. There is a point in touching it only if you are using G-SYNC. All 3D settings are useless. Change the remaining settings in other sections as needed.
 ```
Frequency lock / P-State0
 ```
- We will force P-State 0 using a special parameter in the registry to reduce rendering time and jitter caused by frequency transitions.
 ```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000]
 ```
- This path will not be identical in all cases, the number 0000 is specific to a particular video card and may be overwritten when installing drivers or moving the GPU to a different slot. To determine the appropriate reference number (e.g. 0000, 0001, 0002), open the registry editor and navigate to the path below, then look at the "DriverDesc or HardwareInformation.AdapterString" values, which should contain the adapter name of the graphics card, e.g. NVIDIA GeForce GTX 1050. (timecard).

- Once you know your path, then create a file of type REG.DWORD named DisableDynamicPstate and set the value to 1.

## Lock GPU Clocks/P-State 0

Force P-State 0 with the [registry key](https://github.com/djdallmann/GamingPCSetup/blob/master/CONTENT/RESEARCH/WINDRIVERS/README.md#q-is-there-a-registry-setting-that-can-force-your-display-adapter-to-remain-at-its-highest-performance-state-pstate-p0) below (reboot required). Ensure to change the driver key to the one that corresponds to the correct NVIDIA GPU ([example](/assets/images/find-driver-key-example.png)). This mitigates the undesirable delay to execute new instructions when the unit enters a deeper power-saving state at the expense of higher idle temperatures and power consumption

```bat
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000" /v "DisableDynamicPstate" /t REG_DWORD /d "1" /f
```

# Configure NVIDIA Control Panel

### Manage 3D Settings

> If you are configuring a system for general-purpose use such as for work or school, then skip this step as it is not required.

- Anisotropic filtering - Off

- Antialiasing - Gamma correction - Off

- Low Latency Mode - On/Ultra

    > If a game supports the NVIDIA Reflex Low Latency mode, we recommend using that mode over the Ultra Low Latency mode in the driver. However, if you leave both on, the Reflex Low Latency mode will take higher priority automatically for you ([1](https://www.nvidia.com/en-gb/geforce/news/reflex-low-latency-platform))

- Power management mode - Prefer maximum performance

- Shader Cache Size - Unlimited

- Texture filtering - Quality - High performance

- Threaded Optimization - offloads GPU-related processing tasks on the CPU ([1](https://tweakguides.pcgamingwiki.com/NVFORCE_8.html)). It usually hurts frame pacing as it takes CPU time away from your real-time application. You should also determine whether you are already CPU bottlenecked if you do choose to enable the setting

- Ensure that settings aren't being overridden for programs in the ``Program Settings`` tab, such as Image Sharpening for some EAC games

### Change Resolution

- Output dynamic range - Full

### Adjust Video Color Settings

- Dynamic range - Full

## Game Config setting

> [!CAUTION]
 ```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\System\GameConfigStore]
"GameDVR_Enabled"=dword:00000000
"GameDVR_FSEBehavior"=dword:00000002
"GameDVR_FSEBehaviorMode"=dword:00000002
"GameDVR_HonorUserFSEBehaviorMode"=dword:00000001
"GameDVR_DXGIHonorFSEWindowsCompatible"=dword:00000001
"GameDVR_EFSEFeatureFlags"=dword:00000000
"Win32_AutoGameModeDefaultProfile"=hex:01,00,01,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00
"Win32_GameModeRelatedProcesses"=hex:01,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00

[HKEY_CURRENT_USER\SOFTWARE\Microsoft\GameBar]
"AllowAutoGameMode"=dword:00000000
"AutoGameModeEnabled"=dword:00000000
"GamePanelStartupTipIndex"=dword:00000003
"ShowStartupPanel"=dword:00000000
"UseNexusForGameBarEnabled"=dword:00000000

[HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\GameDVR]
"AppCaptureEnabled"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\GameDVR]
"AllowGameDVR"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\default\ApplicationManagement\AllowGameDVR]
"value"=dword:00000000

[-HKEY_CURRENT_USER\SYSTEM\GameConfigStore\Children]
[-HKEY_CURRENT_USER\SYSTEM\GameConfigStore\Parents]
 ```

## Setting up Nvidia Dwords
 ```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\NVIDIA Corporation\Global\Startup\SendTelemetryData]
@=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\Startup]
"SendTelemetryData"=dword:00000000

[HKLM\SOFTWARE\NVIDIA Corporation\Global\NVTweak]
"DisplayPowerSaving"=dword:00000000

[HKLM\SYSTEM\ControlSet001\Services\nvlddmkm\Global\NVTweak]
"DisplayPowerSaving"=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\NVTweak]
"DisplayPowerSaving"=dword:00000000

[HKLM\SOFTWARE\NVIDIA Corporation\NvControlPanel2\Client]
"OptInOrOutPreference"=dword:00000000

[HKLM\SYSTEM\ControlSet001\Services\nvlddmkm\FTS]
"EnableGR535"=dword:00000000
"EnableRID44231"=dword:00000000
"EnableRID64640"=dword:00000000
"EnableRID66610"=dword:00000000

[HKLM\SYSTEM\ControlSet001\Services\nvlddmkm]
"EnableMidBufferPreemption"=dword:00000000
"DisableCudaContextPreemption"=dword:00000001
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"ComputePreemption"=dword:00000000
"DisablePreemption"=dword:00000001
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"DisableBugcheckCallback"=dword:00000001
"LogWarningEntries"=dword:00000000
"LogPagingEntries"=dword:00000000
"LogEventEntries"=dword:00000000
"LogErrorEntries"=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm]
"EnableMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"ComputePreemption"=dword:00000000
"DisablePreemption"=dword:00000001
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"DisableBugcheckCallback"=dword:00000001
"LogWarningEntries"=dword:00000000
"LogPagingEntries"=dword:00000000
"LogEventEntries"=dword:00000000
"LogErrorEntries"=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]
"DisableWriteCombining"=dword:00000001
"EnablePreemption"=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Control\GraphicsDrivers]
"EnablePreemption"=dword:00000000
"IOMMUFlags"=dword:00000000
"DisableMultiSourceMPOCheck"=dword:00000001
"DisableOverlays"=dword:00000001 
"EnableDecodeMPO"=dword:00000000
"PowerSavingTweaks"=dword:00000000

[HKLM\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Power]
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\NVTweak]
"NvCplAllowWinSatAssessment"=dword:00000000
"NvCplPhysxAuto"=dword:00000000
"NvDevToolsVisible"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm]
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidGfxpSharedBuffer"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"DisablePreemption"=dword:00000001
"DisableWriteCombining"=dword:00000001
"EnableAsyncMidBufferPreemption"=dword:00000001
"EnableBugcheckDisplay"=dword:00000000
"EnableBugcheckTinting"=dword:00000000
"EnableIoMmu"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000001
"EnableMidBufferPreemption"=dword:00000001
"EnableMidGfxPreemption"=dword:00000001
"EnablePageFaultDebugOutput"=dword:00000000
"EnablePerformanceMode"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"DisableBlockWrite"=dword:00000000
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000
"ACGSupported"=dword:00000000
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"TrackResetEngine"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableEventTracer"=dword:00000000
"RMEnableOverclockingAllPstates"=dword:00000001
"RmMIONoPowerOff"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
"TCCSupported"=dword:00000000
"VRRAlwaysON"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0001]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"DisableBlockWrite"=dword:00000000
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000
"ACGSupported"=dword:00000000
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"TrackResetEngine"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableEventTracer"=dword:00000000
"RMEnableOverclockingAllPstates"=dword:00000001
"RmMIONoPowerOff"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
"TCCSupported"=dword:00000000
"VRRAlwaysON"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0002]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"DisableBlockWrite"=dword:00000000
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000
"ACGSupported"=dword:00000000
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"TrackResetEngine"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableEventTracer"=dword:00000000
"RMEnableOverclockingAllPstates"=dword:00000001
"RmMIONoPowerOff"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
"TCCSupported"=dword:00000000
"VRRAlwaysON"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0003]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"DisableBlockWrite"=dword:00000000
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000
"ACGSupported"=dword:00000000
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"TrackResetEngine"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableEventTracer"=dword:00000000
"RMEnableOverclockingAllPstates"=dword:00000001
"RmMIONoPowerOff"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
"TCCSupported"=dword:00000000
"VRRAlwaysON"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0004]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"DisableBlockWrite"=dword:00000000
"ComputePreemption"=dword:00000000
"EnableMidGfxPreemptionVGPU"=dword:00000000
"EnableMidBufferPreemptionForHighTdrTimeout"=dword:00000000
"EnableAsyncMidBufferPreemption"=dword:00000000
"EnableSCGMidBufferPreemption"=dword:00000000
"PerfAnalyzeMidBufferPreemption"=dword:00000000
"EnableMidGfxPreemption"=dword:00000000
"EnableMidBufferPreemption"=dword:00000000
"EnableCEPreemption"=dword:00000000
"EnablePreemption"=dword:00000000
"ACGSupported"=dword:00000000
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"TrackResetEngine"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableEventTracer"=dword:00000000
"RMEnableOverclockingAllPstates"=dword:00000001
"RmMIONoPowerOff"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
"TCCSupported"=dword:00000000
"VRRAlwaysON"=dword:00000000
 ```

## Configure NVIDIA Inspector
> [!CAUTION]
> 📊 **Do not** blindly follow the recommendations in this section. **Do** benchmarks of said changes to ensure that they result in positive performance gains, as every system behaves differently and changes can unintentionally degrade performance.

- Download and extract [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector) Please download my [personal profile](https://drive.google.com/file/d/18PiWZ9HR8BPmGbdr5MyJzn8fwDlbCoxW/view?usp=sharing) and apply it.
