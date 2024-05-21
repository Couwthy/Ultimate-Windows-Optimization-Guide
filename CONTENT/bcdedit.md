# Boot Configuration
- Do not touch settings like useplatformclock, useplatformtick, disabledymanictick, tscsyncpolicy, they are designed for debugging and the system automatically installs them correctly. No need to force the timer to work, just leave it.

## BCDEDIT command - edit Windows boot configuration data.
```
bcdedit /set {globalsettings} custom:16000067 true-Disable the Windows logo at boot time
bcdedit /deletevalue {globalsettings} custom:16000067-return to default
bcdedit /set {globalsettings} custom:16000069 true-Disable animated circle during Windows boot time
bcdedit /deletevalue {globalsettings} custom:16000069-return to default
bcdedit /set {globalsettings} custom:16000068 true
```
## Disable messages during Windows boot
```
bcdedit /deletevalue {globalsettings} custom:16000068-return to default
bcdedit /set {globalsettings} advancedoptions true-enable Windows startup options menu (for experimentation)
bcdedit /deletevalue {globalsettings} advancedoptions true-Default value
bcdedit /set nolowmem Yes - Reduce RAM
bcdedit /deletevalue nolowmem - Reset
bcdedit /deletevalue useplatformclock-disable HPET.
bcdedit /set disabledynamictick yes-This new technology is a grouping, or if you prefer, merging of idle CPU cycles and then processing them only when really needed.
bcdedit /set useplatformtick yes-Disable HPET.
bcdedit /set bootlog no-Disables the system initialization log.
bcdedit /event off-Disables remote event logging for the current Windows operating system boot item
bcdedit /bootdebug off-Disables boot debugging, by default it is enabled.
bcdedit /set vsmlaunchtype Off-This is a protected virtual machine running on the hypervisor and is separate from the host Windows 10 and its kernel.
bcdedit /set bootmenupolicy standart-for the standard boot menu (BLUE screen with options)
bcdedit /set bootmenupolicy legacy-for legacy boot menu (BLACK screen with plain text options)
bcdedit /set tscsyncpolicy enhanced-this is a command for cmd to increase performance, but it will make the inputlag higher.
bcdedit /set tscsyncpolicy legacy-this is to improve inputlag, but will degrade performance (10-20 frames).
bcdedit /deletevalue tscsyncpolicy- default value of the above two commands
bcdedit /set tscsyncpolicy default-value by default
bcdedit /set quietboot yes-a setting that helps or allows quietbooting without outputting any service information.
bcdedit /set debug No-Disables the kernel debugger.

```
