# Post-Install Instructions

- Follow data on young people

# BIOS Configuration:

Consider what Windows version you will be using because some settings listed in this section depend on the Windows version being used (search for *"Windows"* in this section). Read the [What Version of Windows Should You Use?](#102-what-version-of-windows-should-you-use) section to help decide what to use.

## BIOS Recovery Methods

Modifying BIOS is never without risks. Explore methods to flash a stock BIOS such as USB flashback or a [CH341A](https://www.techinferno.com/index.php?/topic/12230-some-guide-how-to-use-spi-programmer-ch341a) programmer if [clearing CMOS](https://www.intel.co.uk/content/www/uk/en/support/articles/000025368/processors.html) does not restore everything to its original state.

## BIOS Updates

Check for BIOS updates and positive changes in the change logs (e.g. increased memory stability). Beware of problems brought up in reviews and forums regarding specific BIOS versions if applicable.

## BIOS Microcode

> [!WARNING]
> 🔒 Upgrading or downgrading microcode may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

On much older platforms and CPUs, BIOS-level Spectre, Meltdown and other CPU microcode patches had the ability to drastically influence performance which isn't so much the case with modern systems nowadays. [CPU-Z's](https://www.cpuid.com/softwares/cpu-z.html) validation feature exposes the microcode version and it was possible to manipulate microcode and their versions within the BIOS using tools such as [MMTool](https://www.ami.com/blog/2017/10/30/what-is-mmtool). Nonetheless, this is not necessarily required to be changed on modern platforms and is here as an informative note.

## Accessing Hidden Options

Motherboard vendors hide and lock a lot of settings so that they aren't visible to a regular user. For clarification, unlocking BIOS corresponds to making hidden settings visible and accessible. The easiest approach to take is to change the access levels within the BIOS using [UEFI-Editor](https://github.com/BoringBoredom/UEFI-Editor#usage-guide) then flash it which will result in hidden options available in the UEFI. An alternative approach is to configure what is already accessible in UEFI then access hidden options by reading and writing to NVRAM using [GRUB](https://github.com/BoringBoredom/UEFI-Editor#how-to-change-hidden-settings-without-flashing-a-modded-bios) or [SCEWIN](https://github.com/ab3lkaizen/SCEHUB).

## Disable Unnecessary Devices

Generally, follow the rule of "If you're not using it, disable it". It is preferable to physically disconnect components if possible, but this typically includes NICs, WLAN, Bluetooth, High Definition Audio (if you are not utilizing motherboard audio) controllers, integrated graphics, SATA, RAM slots, onboard devices visible in [USB Device Tree Viewer](https://www.uwe-sieber.de/usbtreeview_e.html) (e.g. LED controllers, IR receivers) and more. Keep in mind that some motherboards have the High Definition Audio controller linked to the USB controller ([1](https://www.igorslab.de/en/the-old-alc4080-on-the-new-intel-boards-demystified-and-the-differences-from-alc1220-insider)) so don't get confused if this is encountered in the USB device tree.

## Resizable Bar

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

Resizable Bar requires the GPT/UEFI BIOS mode and `Above 4G Decoding` to be enabled. For unsupported motherboards, consider viewing [ReBarUEFI](https://github.com/xCuri0/ReBarUEFI)/[NvStrapsReBar](https://github.com/terminatorul/NvStrapsReBar). To verify that Resizable Bar is enabled, check the status with [GPU-Z](https://www.techpowerup.com/gpuz).

## Hyper-Threading/Simultaneous Multithreading

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

If you have enough CPUs for your application then consider disabling [Hyper-Threading (HT)/Simultaneous Multithreading (SMT)](https://en.wikipedia.org/wiki/Hyper-threading). This feature is beneficial for highly threaded operations such as encoding, compiling and rendering however using multiple execution threads per CPU increases contention on processor resources and is a potential source of system latency and jitter ([1](https://www.intel.com/content/www/us/en/developer/articles/technical/optimizing-computer-applications-for-latency-part-1-configuring-the-hardware.html)). Disabling HT/SMT has the additional benefit of increased overclocking potential due to lower temperatures in which, a similar concept can be applied to Intel's E-Cores (efficiency cores) however, both can affect performance positively or negatively in some games hence, I would recommend benchmarking these options thoroughly and not blindly disabling them.

## Power States

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

To be completed.

## Virtualization/SVM Mode

Disable [Virtualization/SVM Mode](https://en.wikipedia.org/wiki/Desktop_virtualization) and [Intel VT-d/AMD-Vi](https://en.wikipedia.org/wiki/X86_virtualization#I/O_MMU_virtualization_(AMD-Vi_and_Intel_VT-d)) if applicable as they can cause a difference in latency for memory access ([1](https://www.amd.com/system/files/TechDocs/56263-EPYC-performance-tuning-app-note.pdf)). Virtualization also has the potential to affect BCLK ([1](https://linustechtips.com/topic/1479168-issue-enabling-svm-virtualization-causes-bclk-to-fluctuate-a-lot)). The virtualization status can be verified using Task Manager's CPU section.

## Power-Saving

Power-saving has no place on a machine executing real-time tasks. These features can be named differently, including but not limited to [ASPM (Active State Power Management)](https://en.wikipedia.org/wiki/Active_State_Power_Management) (e.g. search for *L0*, *L1*), [ALPM (Aggressive Link Power Management)](https://en.wikipedia.org/wiki/Aggressive_Link_Power_Management), DRAM Power Down Mode, Power/Clock Gating and more. You can also look out for options named *power management* or *power saving*. Search the internet if you are unsure whether a given setting is power-saving related.

## Trusted Platform Module (TPM)

> [!WARNING]
> 🔒 Disabling TPM may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

Disable Trusted Platform Module as it may cause the system to enter System Management Mode (SMM) via System Management Interrupts (SMIs) ([1](https://youtu.be/X72LgcMpM9k?si=A5Kl5NmU5f1WzZP4&t=2060)) which are high priority unmaskable hardware interrupts which cause the CPU to immediately suspend all other activities, including the operating system ([1](https://wiki.linuxfoundation.org/realtime/documentation/howto/debugging/smi-latency/smi)). On Windows 11, a minority of anticheats (Vanguard, FACEIT) require it to be enabled and its status can be verified by typing ``tpm.msc`` in ``Win+R``.

## Compatibility Support Module (CSM)

MBR/Legacy requires Compatibility Support Module to be enabled and typically, only the storage and PCIe OpROMs are required, but you can enable all of them if you are unsure. Disable CSM if you are using GPT/UEFI with the exception being Windows 7 GPT/UEFI as it requires CSM and OpROMs unless you are using [uefiseven](https://github.com/manatails/uefiseven).

## Secure Boot

> [!WARNING]
> 🔒 Disabling Secure Boot may negatively impact security and expose the system to vulnerabilities. Users should evaluate the security risks associated with modifying the specified setting.

On Windows 11, a minority of anticheats (Vanguard, FACEIT, THE FINALS) require Secure Boot to be enabled. If something fails due to Secure Boot being enabled such as bootable tools, I recommended temporarily disabling it rather than resorting to alternative solutions such as enrolling keys as they can lead to issues. If Secure Boot is not required, it can be disabled to avoid various issues. Its status can be verified by typing ``msinfo32`` in ``Win+R``.

## Fast Startup, Standby and Hibernate

This boils down to personal preference, perceptions and experiences however, some individuals prefer not to utilize features such as Fast Startup, standby and hibernation, as they can lead to unexpected issues ([explanation](https://www.youtube.com/watch?v=OBGxt8zhbRk)), while preferring to perform clean system boots instead of saving and restoring kernel and software state thus limiting the system power states to S0 (working state) and S5 (soft off). Learn about system power states and their meaning [here](https://learn.microsoft.com/en-us/windows/win32/power/system-power-states) and [here](https://www.sciencedirect.com/topics/computer-science/sleeping-state). These options in BIOS are often named Fast Startup, Suspend to RAM, S-States (search for *S1*, *S2*, *S3*, *S4*, *S5*), standby or similar options. S-State status can be verified with ``powercfg /a`` in CMD.

Windows also has a toggle that disables Fast Startup, hibernation and removes ``C:\hiberfil.sys``:

```bat
powercfg /h off
```

## Spread Spectrum

Disable Spread Spectrum and ensure BCLK frequency is close to the desired value as possible (e.g. 100.00MHz not 99.97MHz) in [CPU-Z](https://www.cpuid.com/softwares/cpu-z.html) however, this highly dependent on the system and motherboard.

## Legacy USB Support

Disable Legacy USB Support as it may cause the system to enter System Management Mode (SMM) via System Management Interrupts (SMIs) ([1](https://patents.google.com/patent/US6067589), [2](https://www.kernel.org/doc/Documentation/x86/usb-legacy-support.txt)) which are high priority unmaskable hardware interrupts which cause the CPU to immediately suspend all other activities, including the operating system ([1](https://wiki.linuxfoundation.org/realtime/documentation/howto/debugging/smi-latency/smi)). You may need to turn this on to install a new operating system, access BIOS or USB devices in some cases.

## Disable Software Installation Options

If there are options relating to software installation (e.g. ASUS Armoury Crate), then disable them. These types of software are typically in-line with other bloatware which can safely be avoided and are present in various BIOSes ([ASUS](https://www.asus.com/support/faq/1043788), [Gigabyte](https://old.reddit.com/r/gigabyte/comments/106d9ns/gigabyte_control_center_prompt_to_install_every/ja0gc6l), [MSI](https://old.reddit.com/r/MSI_Gaming/comments/14s7so7/how_to_disable_autoinstall_of_msi_center/l6zoigh), [ASRock](https://old.reddit.com/r/ASRock/comments/1bxf8jt/asrock_auto_driver_install_app/kyc904r)).

## Configure PCI Link Speed for Devices

Set PCIe link speed to the maximum supported such as ``Gen 4.0``. This may be represented as gigatransfers per second (GT/s) ([1](https://en.wikipedia.org/wiki/PCI_Express#Comparison_table)). This helps with alleviating unexpected behavior and issues.

## Fan Curves

To maximize cooling potential, configure fan curves ([example](https://imgur.com/a/2UDYXp0)) or set a static, high, noise-acceptable RPM. Set your AIO pump speed to full if applicable.

## BIOS Profiles and Backups

Backup BIOS by saving the current settings to a profile or export one to local storage as clearing CMOS will wipe all settings if you need to do so (e.g. while overclocking).

In my experience on various motherboards, loading a saved profile fails to restore certain settings after clearing CMOS. I would recommend dumping NVRAM using a tool such as [SCEWIN](https://github.com/ab3lkaizen/SCEHUB) so that when you restore a profile, dump NVRAM again then compare it to the previous/original export to see whether anything failed to restore by using a text comparison tool such as the [Notepad++ Compare plugin](https://sourceforge.net/projects/npp-compare) or [Visual Studio Code](https://code.visualstudio.com/download).

---

# Configure USB Port Layout

## Assess Accessible USB Ports

Firstly, familiarize yourself with which USB ports correspond to given USB controllers as some ports shown in [USB Device Tree Viewer](https://www.uwe-sieber.de/usbtreeview_e.html) may not be physically accessible. I recommended plugging a device into every accessible port on your system such as the ones on the motherboard I/O and front panels, then take a note of which controller and port each physical port corresponds to in USB Device Tree Viewer

## Layout Planning

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

Secondly, plan and decide which USB controllers you would like to plug devices into but don't plug them in yet. As for which USB controllers should be used, that is up to you. If you have more than one USB controller, you can isolate devices such as your mouse, keyboard and audio devices onto another USB controller as they have the potential to interfere with polling consistency ([1](https://forums.blurbusters.com/viewtopic.php?f=10&t=7618#p58449)). More USB controllers may be made available by using PCIe expansion cards or external USB 2.0 and 3.0 headers on your motherboard. Always verify with [USB Device Tree Viewer](https://www.uwe-sieber.de/usbtreeview_e.html). Ryzen systems have a USB controller that is directly connected to the CPU ([1](https://hexus.net/tech/features/mainboard/131789-amd-ryzen-3000-supporting-x570-chipset-examined)) which can be identified under the PCIe Bus category in [HWiNFO](https://www.hwinfo.com). It is usually the USB controller that is connected to an ``Internal PCIe Bridge to bus`` which is also labelled with the CPU architecture ([example](/assets/images/ryzen-cpu-usb-controller.png)).

## Plugging In Devices

Lastly, plug the devices into the ports and USB controllers that you have decided to use. In any case, consider populating ones that are closest to the root of the USB controller's hub tree first. Additionally, I would also recommend avoiding internal hubs ([example](/assets/images/usb-hub-internal-headers.png)).

---

# Configure Peripherals

## Cleaning

Carefully use an [air dust blower](https://www.amazon.com/s?k=air+dust+blower) to remove dirt and debris from the mouse sensor lens without damage.

## Configure Onboard Memory Profiles

Most modern peripherals support onboard memory profiles such as mice and keyboards. Configure them before configuring the OS as you will not be required to install the bloatware such as Razer Synapse to change the settings later. Details for separating bloat-free and bloated environments using a dual-boot will be discussed in later steps. Alternatively, limit the bloated software to a bootable Windows USB ([Windows To Go](https://www.youtube.com/watch?v=w34x1kBZN6c)).

## Disable RGB Lighting Effects

USB 2/3 are limited to 0.5A/0.9A respectively ([1](https://en.wikipedia.org/wiki/USB)) and RGB requires unnecessary power. Turn off lighting effects or strip the LED from the peripheral as running an RGB effect/animation can take a great toll on the MCU and will delay other processes ([1](https://wooting.io/post/what-influences-keyboard-speed), [2](https://www.techpowerup.com/review/endgame-gear-xm1-rgb/5.html#:~:text=tracking%20quality%20takes%20a%20hit%20as%20soon%20as%20RGB%20is%20enabled), [3](https://www.techpowerup.com/review/roccat-kone-pro-air/5.html#:~:text=after%20having%20disabled%20all%20RGB%20lighting,%20these%20outliers%20disappeared%20entirely)).

## DPI

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

Higher sensor DPI reduces latency and helps in saturating polls with motion data ([1](https://www.youtube.com/watch?v=6AoRfv9W110), [2](https://www.youtube.com/watch?v=mwf_F2VboFQ&t=458s), [3](https://www.youtube.com/watch?v=imYBTj2RXFs&t=275s)). Avoid jitter reduction and [sensor smoothing](https://old.reddit.com/r/MouseReview/comments/5haxn4/sensor_smoothing) kicking in with higher DPI values. If your game uses raw input, you can [reduce the pointer speed](https://boringboredom.github.io/tools/winsenscalculator) in Windows to offset the sensitivity from higher DPI. Otherwise, leave the slider at the default position as input will be negatively affected due to scaling. One way to determine whether a given application is using raw input is to spy on the raw input API calls with [API Monitor](http://www.rohitab.com/apimonitor) or check whether the ``enhance pointer precision`` option has any effect in-game. If you are still unsure or have doubts, leave the slider at the default position.

## Report Rate

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

Higher polling rates reduce jitter and latency ([1](https://www.youtube.com/watch?app=desktop&v=djCLZ6qEVuA), [2](https://www.youtube.com/watch?v=mwf_F2VboFQ&t=458s), [3](https://www.youtube.com/watch?v=mwf_F2VboFQ&t=618s)). Higher polling rates may negatively impact performance depending on your hardware and general configuration so adjust accordingly.

## Polling Stability Analysis

Use Mouse Tester to check whether each poll contains data. As an example, if the interval is spiking to 2ms (500Hz) or higher from 1ms (1kHz), this is problematic and may be due to several variables such as the device itself (e.g. sensor fault), cable, power issues, hardware, operating system and more. You may need to lower or disable USB interrupt moderation using this script if there are multiple devices generating interrupts on the same USB controller and/or the mouse interrupts are being generated at a rate greater than or equal to the default IMOD interval during the benchmark resulting in IMOD kicking in.

## Monitor

Optionally reset your monitor to factory settings and reconfigure it in case anything was misconfigured initially. Overdrive/AMA reduces latency ([1](https://twitter.com/CaIypto/status/1464236780190851078)) however, it comes with the penalty of additional overshoot. Additionally, you can attempt to calibrate it. Optionally overclock your display with [Custom Resolution Utility](https://www.monitortests.com/forum/Thread-Custom-Resolution-Utility-CRU) and test for [frame skipping](https://www.testufo.com/frameskipping). Aim for an `actual` integer refresh rate such as 60.00/240.00, not 59.94/239.76.

- See [Can You Calibrate a Monitor WITHOUT a Colorimeter? | techless](https://www.youtube.com/watch?v=avJTz1JhkR4)

---

# Stability, Hardware Clocking and Thermal Performance

Ensure that all of your hardware is stable before configuring a new operating system as unstable hardware can lead to crashes, data corruption, worse performance or indirectly irreversible damage to hardware. The effectiveness of testing for instability varies between tools which is why it is important to use a range of them for a sufficient amount of time (a non-exhaustive list of recommended tools is listed below).

## Temporary Operating System

I would highly recommend configuring a temporary dual-boot with a fresh installation of Windows or a bootable Windows USB ([Windows To Go](https://www.youtube.com/watch?v=w34x1kBZN6c)) to avoid corrupting your main operating system while stress-testing and overclocking. In terms of memory stress-testing, this also allows the stress-test to use more RAM as it isn't being hogged by potential bloatware on your current installation. Safe mode can also serve as a minimal testing environment but certain software may not work.

## General Information

- Verify and validate changes within software to avoid unexpected results and behavior (e.g. frequency, voltages, timings)

- Save a BIOS profile before each change when overclocking such as changing CPU/RAM frequency and RAM timings so that you don't lose progress if you need to clear CMOS. Refer to the [BIOS Profiles and Backups](#622-bios-profiles-and-backups) section regarding restoring settings properly

- When overclocking, you may be required to raise various power limits if the default limits are exceeded

- Use [HWiNFO](https://www.hwinfo.com) to monitor system sensors. A higher polling interval can help to identify sudden spikes but not transients on a microsecond scale as an example. Avoid running while benchmarking as it has the potential to reduce the reliability of results

- A single error or crash is one too many. Monitor WHEAs with [HWiNFO](https://www.hwinfo.com)'s error count or configure an Event Viewer filter

- Monitor voltages where applicable due to potential overvolting

- There are countless factors that contribute to stability such as temperature, power delivery, quality of hardware in general, silicon lottery and more

## Error Correction

Overclocking does not necessarily mean that the system will perform better due to factors such as error correction where applicable. You should verify whether whatever you are changing scales positively by adopting a systematic benchmarking methodology.

## Thermal Management

Avoid thermal throttling at all costs. As a reminder, ambient temperature will generally increase during the summer. Deliberately underclock if your cooler is inadequate. A thermally stable component with an overall lower frequency is preferable compared to thermal throttling at a higher frequency/voltage. To apply additional thermal stress when tuning any component (e.g. CPU, RAM, GPU), consider turning off case, RAM fans or reducing RPM along with generating extra heat (e.g. GPU load, room heaters) while stress-testing.

- See [RAM Overclock Stability and Heat Management | buildzoid](https://www.youtube.com/watch?v=iCD0ih4qzHw)

## Load-line Calibration

This is not a recommendation of what LLC mode to use and is instead, here for informative purposes.

- See [VRM Load-Line Visualized | ElmorLabs](https://elmorlabs.com/2019-09-05/vrm-load-line-visualized)
- See [Vdroop setting and it’s impact on CPU operation | xDevs](https://xdevs.com/guide/e399ocg/#vdroop)
- See [Why Vdroop is good for overclocking and taking a look at Gigabyte's Override Vcore mode | buildzoid](https://www.youtube.com/watch?v=zqvNkh4TVw8)

## GPU

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

When overclocking the GPU, you may be required to flash a BIOS with a higher power limit or raise them.

- On NVIDIA systems, ensure to disable ``CUDA - Force P2 State`` with [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector) to prevent memory downclocking while stress-testing
- See [A Slightly Better Way To Overclock and Tweak Your Nvidia GPU | Cancerogeno](https://docs.google.com/document/d/14ma-_Os3rNzio85yBemD-YSpF_1z75mZJz1UdzmW8GE/edit)
- See [LunarPSD/NvidiaOverclocking](https://github.com/LunarPSD/NvidiaOverclocking/blob/main/Nvidia%20Overclocking.md)

## RAM/CPU

> [!CAUTION]
> 📊 **Do NOT** blindly follow the recommendations in this section. **Do** benchmark the specified changes to ensure they result in positive performance scaling, as every system behaves differently and changes could unintentionally degrade performance ([instructions](#3-benchmarking)).

- Ensure that your CPU is able to boost correctly before starting in case you have disabled options such as SpeedStep and Speed Shift which can prevent the processor from exceeding its base frequency

- Configure RAM frequency and timings manually for a significant performance improvement ([1](https://kingfaris.co.uk/blog/intel-ram-oc-impact)). XMP does not tune many timings nor does it guarantee stability

  - See [Eden’s DDR4 guide](https://web.archive.org/web/20231211232729/https://cdn.discordapp.com/attachments/328891236918493184/1172922515962724444/DDR4_Guide_V1.2.1.pdf)
  - See [KoTbelowall/INTEL-DDR4-RAM-OC-GUIDE-by-KoT](https://github.com/KoTbelowall/INTEL-DDR4-RAM-OC-GUIDE-by-KoT)
  - See [integralfx/MemTestHelper](https://github.com/integralfx/MemTestHelper/blob/oc-guide/DDR4%20OC%20Guide.md)

- Configure static all-core frequencies and voltages for the CPU. Variations in hardware clocks can introduce jitter due to the process of frequency transitions. [Precision Boost Overdrive](https://www.amd.com/en/support/kb/faq/cpu-pb2) for Ryzen CPUs is an alternative option to a static frequency and voltages and is often recommended

- The previous two bullet points affect each other in terms of stability which means that your RAM overclock may become unstable after tuning the CPU, so run RAM stress-tests again and adjust your CPU settings if required

## Stress-Testing Tools

- StresKit (bootable)

- Linpack

  - StresKit's Linpack
  - [Linpack-Extended](https://github.com/BoringBoredom/Linpack-Extended)
  - [Linpack Xtreme Bootable](https://www.techpowerup.com/download/linpack-xtreme)
  - Use a range of memory sizes
  - Residuals should match otherwise, it may be a sign of instability
  - GFLOP variation should be minimal

- [Prime95](https://www.mersenne.org/download)

- [FIRESTARTER](https://github.com/tud-zih-energy/FIRESTARTER)

- [y-cruncher](http://www.numberworld.org/y-cruncher)

- [Memory Testing Software](https://github.com/integralfx/MemTestHelper/blob/oc-guide/DDR4%20OC%20Guide.md#memory-testing-software)

  - [HCI](https://hcidesign.com/memtest)
  - [MemTest86](https://www.memtest86.com) (bootable)
  - [MemTest86+](https://memtest.org) (bootable)

- [UNIGINE Superposition](https://benchmark.unigine.com/superposition)

- [OCCT](https://www.ocbase.com)

- [memtest_vulkan](https://github.com/GpuZelenograd/memtest_vulkan)

---

## Choosing the Windows Version

- The choice between Windows 10 and Windows 11 should be based on several key factors, including technical requirements, functional preferences and specific user needs.

### Recommendations for Choosing the Windows Version:

- Windows 11: Recommended for Ryzen 7800x3d, 7900x3d, 7950x3d and Intel 12-14 generation processors with E-cores. Windows 11 offers improved support for the latest hardware and is optimized for modern gaming technologies such as Auto HDR and DirectStorage.
- Windows 10: Is the preferred choice for all other scenarios. Windows 10 continues to be a reliable and stable system for a wide range of hardware and gaming applications, providing high compatibility and performance.

## Configure Storage Partitions

Set up a [multi-boot](https://en.wikipedia.org/wiki/Multi-booting) system to maintain separate environments for work/bloatware and gaming, ensuring the latter one remains free of bloatware. This allows you to keep the gaming partition clean and free of unnecessary software, as discussed in earlier sections. By doing so, you avoid installing bloatware on the same partition where you use real-time applications without sacrificing usability. To achieve this, shrink a volume in Disk Management ([instructions](https://docs.microsoft.com/en-us/windows-server/storage/disk-management/shrink-a-basic-volume)) to create unallocated space for installing the new operating system.

## What Version of Windows Should You Use?

- Earlier versions of Windows lack anticheat support (due to lack of security updates from end-of-life OSes), driver support (commonly GPU, NIC) and application support in general, so some users are forced to use newer builds. See the table below of the minimum version required to install drivers for given GPUs

    |GPU|Minimum Windows Version|
    |---|---|
    |NVIDIA 10 series and lower|Supported by almost all Windows versions|
    |NVIDIA 16, 20 series|Win7, Win8, Win10 1709+|
    |NVIDIA 30 series|Win7, Win10 1803+|
    |NVIDIA 40 series|Win10 1803+|
    |AMD|Refer to driver support page|

- Windows Server lacks support for a lot of consumer NICs. Workaround tends such as [this](https://github.com/loopback-kr/Intel-I219-V-for-Windows-Server) tend to interfere with anticheats due to invalid signing certificates

- NVIDIA DCH drivers are supported on Windows 10 1803+ ([1](https://nvidia.custhelp.com/app/answers/detail/a_id/4777/~/nvidia-dch%2Fstandard-display-drivers-for-windows-10-faq))

- During media playback exclusively on Windows 10 1709, the [Multimedia Class Scheduler Service](https://learn.microsoft.com/en-us/windows/win32/procthread/multimedia-class-scheduler-service) raises the timer resolution to 0.5ms which limits control regarding the requested resolution

- Windows 10 1809+ is required for Ray Tracing on NVIDIA GPUs

- Microsoft implemented a fixed 10MHz QueryPerformanceFrequency on Windows 10 1809+

- Windows 10 1903+ has an updated scheduler for multi CCX Ryzen CPUs ([1](https://i.redd.it/y8nxtm08um331.png))

- DirectStorage requires Windows 10 1909+ but according to an article, games running on Windows 11 benefit further from new storage stack optimizations ([1](https://devblogs.microsoft.com/directx/directstorage-developer-preview-now-available))

- Windows 10 2004+ is required for [Hardware Accelerated GPU Scheduling](https://devblogs.microsoft.com/directx/hardware-accelerated-gpu-scheduling) which is necessary for DLSS Frame Generation ([1](https://developer.nvidia.com/rtx/streamline/get-started))

- Processes raising the timer resolution on Windows 10 2004+ no longer affect the global timer resolution ([1](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timebeginperiod), [2](https://randomascii.wordpress.com/2020/10/04/windows-timer-resolution-the-great-rule-change)) meaning that it is set on a per-process basis in which, processes that do not explicitly raise the resolution are not guaranteed a higher resolution and are serviced less often. This was further developed on Windows 11 as a higher resolution is not guaranteed to the calling process if its window is minimized or visibly occluded ([1](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timebeginperiod)). Microsoft added the ability to restore the global behavior on Windows Server 2022+ and Windows 11+ with a registry entry ([1](https://randomascii.wordpress.com/2020/10/04/windows-timer-resolution-the-great-rule-change)) meaning that the implementation can not be restored on Windows 10 versions 2004 - 22H2

- Windows 11+ has an updated scheduler for Intel 12th Gen CPUs and above ([1](https://www.anandtech.com/show/16959/intel-innovation-alder-lake-november-4th/3)) but the behavior can be replicated manually with affinity policies on any Windows version as explained in later sections

- Windows 11+ limits the window message rate of background processes ([1](https://blogs.windows.com/windowsdeveloper/2023/05/26/delivering-delightful-performance-for-more-than-one-billion-users-worldwide))

- Windows 11 is a minimum requirement for [Cross Adapter Scan-Out](https://videocardz.com/newz/microsoft-cross-adapter-scan-out-caso-delivers-16-fps-increse-on-laptops-without-dgpu-igpu-mux-switch) ([1](https://devblogs.microsoft.com/directx/optimizing-hybrid-laptop-performance-with-cross-adapter-scan-out-caso))

- AllowTelemetry can be set to 0 on Windows Server editions ([1](https://admx.help/?Category=Windows_10_2016&Policy=Microsoft.Policies.DataCollection::AllowTelemetry))

## Download and Prepare a Stock Windows ISO

In order to install Windows, an installation media must be created using an ISO file. Upon downloading ISOs, ensure to cross-check the hashes for the file with official sources to verify that it is genuine and not corrupted. Use the command ``certutil -hashfile <file>`` in CMD to obtain the hashes of the file.

Ensure to download an ISO that contains an edition with group policy support as several policies are configured in later steps. Sometimes, you can get ISOs with specific editions missing so be careful. Below is a list of recommended editions.

- Client editions: Professional
- Server editions: Standard (Desktop Experience)

## ISO Sources

- [os.click](https://os.click)
- [New Download Links](https://docs.google.com/spreadsheets/d/1zTF5uRJKfZ3ziLxAZHh47kF85ja34_OFB5C5bVSPumk)
- [Adguard File List](https://files.rg-adguard.net)
- [Microsoft Software Download Listing](https://massgrave.dev/msdl)
- [Fido](https://github.com/pbatard/Fido)
- [UUP dump](https://uupdump.net)

## Boot Into the ISO

This section covers booting into the ISO retrieved and prepared in the previous section. For the next steps, you are required to disconnect the Ethernet cable and not be connected to the internet during the installation process. This will allow us to bypass the forced Microsoft login during OOBE, allowing us to use Windows with a local account along with preventing installation of unwanted updates and drivers. There are two options when it comes to installing Windows, installing using USB storage or using DISM (without USB storage). Either option can be used. The latter option requires dual-booting.

<details>
<summary>Option 1 -  Install using USB storage</summary>

- Download [Ventoy](https://github.com/ventoy/Ventoy/releases) and launch ``Ventoy2Disk.exe``. Navigate to the option menu and select the correct partition style and disable Secure Boot support. The current partition style can be determined by typing ``msinfo32`` in ``Win+R``. Finally, select your USB storage and click install. If you want to remove your current operating system and wipe the entire drive, then you will have to install using USB storage

- Move your Windows ISO into the USB storage in File Explorer

- If Secure Boot is enabled, temporarily disable it for the installation process. Boot into Ventoy on your USB in BIOS and select your Windows ISO. Continue with setup as per usual. Once setup has finished, Secure Boot can be re-enabled if you had temporarily disabled it

- When installing Windows 8 with a USB, you may be required to enter a key. Use the generic key ``GCRJD-8NW9H-F2CDX-CCM8D-9D6T9`` to bypass this step. This does not activate Windows

- When installing Win11 with a USB, you may encounter system requirement issues. To bypass the checks, press ``Shift+F10`` to open CMD then type ``regedit`` and add the relevant registry keys listed below

    ```
    [HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig]
    "BypassTPMCheck"=dword:00000001
    "BypassRAMCheck"=dword:00000001
    "BypassSecureBootCheck"=dword:00000001
    ```

</details>

<details>
<summary>Option 2 -  Install using DISM Apply-Image (without USB storage)</summary>

- As this method requires specifying an existing partition to apply the ISO to, create a new partition by [shrinking a volume](https://docs.microsoft.com/en-us/windows-server/storage/disk-management/shrink-a-basic-volume) if you haven't already, then assign the newly created unallocated space a drive letter

- Extract the ISO if required then run the command below to apply the image to a given partition. Replace ``<path\to\wim>`` with the path to the ``install.wim`` or ``install.esd`` in each command

  - Get all available editions and their corresponding indexes

      ```bat
      DISM /Get-WimInfo /WimFile:<path\to\wim>
      ```

  - Apply the image by replacing ``<index>`` with the index of the desired edition and ``<drive letter>`` with the drive letter you assigned in the previous step for the image to be mounted on (e.g. index ``1`` and drive letter ``D:``)

      ```bat
      DISM /Apply-Image /ImageFile:<path\to\wim> /Index:<index> /ApplyDir:<drive letter>
      ```

- Create the boot entry with the command below. Replace ``<windir>`` with the path to the mounted ``Windows`` directory (e.g. ``D:\Windows``)

    ```bat
    bcdboot <windir>
    ```

- The installation process will begin after a system restart

</details>

---

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

# Configuring the Power Supply to Optimize Performance

### Choosing An Energy-Saving Plan

- For AMD and Intel processors of 12-14 generations: It is recommended to use the "Balanced" plan. For Ryzen users, don't forget to set the slider to the "Best Performance" position through the Windows Power Settings panel. For older Intel processors (11th generation and below): Enable the Ultimate Performance plan to maximize productivity.

### Open the command prompt as an administrator:

- Press Win + X and select "Command Prompt (Administrator)" or "Windows PowerShell (Administrator)".
- Enter the command to activate the plan:

 ```
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
```

### Configuring USB Settings to Save Energy

- Set the value to "Forbidden" to prevent temporary disconnection of USB ports, which can be useful for connected gaming devices and peripherals that require constant


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
