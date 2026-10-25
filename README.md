# LG K7 source kernel for CM13

**2026-10-25: source-built kernel qualified in the enforcing CM13 ROM on
MetroPCS MS330.** Branch `bringup/cm13-m1`, 32-bit ARM,
`m1_mpcs_us-perf_defconfig`. Other K7 variants remain unqualified.

Use matching [product](https://github.com/airi-kozume/cyanogenmod_device_lge_m1/tree/bringup/cm13-m1),
[common](https://github.com/airi-kozume/android_device_lge_m1-common/tree/resurrection/cm13-static-audit)
and [vendor](https://github.com/airi-kozume/proprietary_vendor_lge_m1/tree/bringup/cm13-m1)
branches. The product README is the current hardware matrix.

## Qualified integration

The Android-M policy29/30/ioctl compatibility and rootfs-labeling backports boot
SELinux enforcing with the matching device policy. Existing userdebug exceptions
remain individually permissive; the system is not globally permissive. Installed
18 kernel modules pass release/vermagic and symbol-CRC compatibility audits.

The combined ROM boots normally and supports display/touch/navigation, Wi-Fi
persistence, Bluetooth automatic reconnect/A2DP, speaker audio, both cameras'
photos and video/audio, flash, rotation, hardware H.264 playback, MTP/PTP with
and without ADB, and GPS/Maps. Overnight idle has shown no observed problems.
These are combined-ROM results; matching userspace and vendor integration matter.
The earlier WCNSS watchdog panic has not returned in qualified testing.

## Remaining scope

Active-SIM cellular data and normal-use battery endurance await testing. SIM
detection/IMEI/baseband are established. Calls/call audio are outside scope:
VoLTE is unsupported and local networks require it. USB OTG is unsupported on
this device. Longer workload and detailed GPS-status checks are separate from
basic functionality. Overnight idle is not a measurement of suspend residency.

Surrounding workspace audits check kernel/image hashes, ramdisk/policy, module
installation, partition limits and actual signed OTA payloads. Preserve hashed
rollback packages. Upstream Linux [README](README) and [COPYING](COPYING)
remain unchanged.
