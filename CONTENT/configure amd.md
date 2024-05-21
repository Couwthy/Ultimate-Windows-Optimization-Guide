# Configure the AMD Driver

- Go to [website](https://www.amd.com/en/support), select your card, download the latest recommended (WHQL) driver, unzip it into a folder.

- Move ``Packages\Drivers\Display\XXXX_INF`` to the Desktop (the folder may be named differently in other driver versions). Delete all but the following:

- In the driver directory folder (mine is B381690 in the example above), move the ccc2_install.exe file to the Desktop. It will be used in the next step.

- Open the Notepad file and save it as ccc2_install.exe in the driver folder.

- Open Device Manager and install the driver by right-clicking on the display adapter, browse my computer for driver software and select the driver folder.

- After installing the driver, unzip ccc2_install.exe with 7-Zip and run ``CN\cnext\cnext64\ccc-next64.msi`` to install the radeon software control panel.

- Make sure to disable AMD bloatware services in win+r, services.msc

### Configuring the AMD Control Panel

```
Texture filtering quality - Performance
Tessellation Mode - Override application settings
Maximum tessellation level - Off.
```
```
FreeSync - could potentially increase input lag due to the extra processing, however it has supposedly improved over time, so feel free to test this yourself, your results may vary
GPU Scaling - Off
HDCP Support - Disable (required for DRM content)
```
```
Lock frequency/P-State 0
```

- Use OverdriveNTool or MorePowerTool to reduce render times and jitter caused by frequency transitions

### RadeonMod

- Run the utility, select your video card, go to the 0000 panel, find the Power Saving tab, the Enable Ulps parameter and set it to 0.
