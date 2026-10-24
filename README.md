# LG K7 source kernel for CM13 bring-up

**Status, 2026-10-24: source-built kernel boots the working LG K7 MS330 port.**
Branch: `bringup/cm13-m1`. The qualified configuration is 32-bit ARM with
`m1_mpcs_us-perf_defconfig`, selected by the matching product device tree.
Other K7 variants are not qualified by this work.

Use this with the matching
[product](https://github.com/airi-kozume/cyanogenmod_device_lge_m1/tree/bringup/cm13-m1),
[common device](https://github.com/airi-kozume/android_device_lge_m1-common/tree/resurrection/cm13-static-audit)
and [vendor](https://github.com/airi-kozume/proprietary_vendor_lge_m1/tree/bringup/cm13-m1)
branches. The product README contains the full runtime status.

## Confirmed in the combined port

- Clean installation boots normally to the launcher.
- Display, touch, backlight, navigation and battery reporting are restored.
- Wi-Fi Internet access and Bluetooth/A2DP operate, including concurrent use;
  the previously observed WCNSS watchdog panic has not returned in these tests.
- Rear/front still capture, sensors/rotation and rear video/audio recording work
  with the selected device/vendor components.
- SIM detection, IMEI and baseband are established; live data service is pending.

These are combined-ROM results, not a claim that kernel code alone provides
the corresponding userspace services or that every kernel feature is tested.

## Remaining work

SELinux is unresolved. The boot-tested `cm_m1_radio_noselinux` product disables
it; the kernel/policy version mismatch still needs investigation before the
SELinux-enabled product can be qualified. Live cellular service requires an
active compatible SIM. GPS, suspend/battery endurance and longer workloads
remain validation items. The previous blanket “no known issues” claim was too
broad and is superseded by this status.

Kernel/image hashes, ramdisk contents, module installation and partition bounds
are checked in the surrounding bring-up workspace. Preserve its known-good ZIPs
when testing policy or kernel changes. The upstream Linux [README](README) and
[COPYING](COPYING) remain unchanged.
