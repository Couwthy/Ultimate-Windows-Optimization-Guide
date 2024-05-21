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
- Run the setup.exe file and install the driver.

### Настройка видеодрайвера

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

## Configure NVIDIA Inspector

- Download and extract [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector) Please download my [personal profile](https://drive.google.com/file/d/1gAX-wmDWFIAM-yqWD90u6LfGKK_VEm48/view?usp=sharing) and apply it.
