# MS330 CM12.1 custom-kernel experiment

This independent local clone starts at FenomenalMOD-m1
1ed04d230d2b42a12fda07eb6c8592e6c1b500d1. The original custom_kernel_src
checkout and the existing CM12/CM13 kernel checkouts are preserved.

The stock-working kernel's commit lineage is known; this source build is not
claimed to reproduce its exact binary. Use m1_mpcs_us-perf_defconfig and the
existing ARM GCC4.8 inside the project's Trusty chroot. Build output lives outside
this repository under audit/cm12-port/boot-failure/kernel-reference/custom-cm12-build.
The workspace tools/build_cm12_custom_kernel_in_trusty.sh reproduces the build.

## Applied adaptations

Commit b5e86e47 ports the two hardware fallbacks previously qualified with CM13:

- MPCS MIT200 touch initializes from controller firmware when CM ships no firmware
  update image. Keep the failed controller-read check; do not force firmware flash.
- VM-BMS initializes voltage-derived state of charge and resumes monitoring when
  the stock userspace BMS daemon does not open the device. Retry failed calculations.

These depend on the device/userspace contract rather than Android 6 interfaces.
Application is source-reviewed; hardware behavior on CM12 remains unqualified.

## Deliberately excluded

Do not import the Android-M policy29/30/ioctl/rootfs backport for this experiment.
CM12's actual compiled policy is version26; this baseline supports through28.
Keep the custom reference's configuration, compiler accommodations, existing
security changes and drivers. No CM13 RIL shim or GPS adapter belongs in the kernel.

All 18 previously sampled Binder/ashmem/ION/KGSL/display/audio interface headers
match the existing CM12 kernel. That is a bounded interface check, not complete ABI
certification. Build matching modules and audit their actual symbol CRCs before
claiming compatibility with any installed system modules.

## Testing and recovery

Use native CM12 init/ramdisk with explicit early diagnostic ADB for boot isolation.
Preserve the stock DT and boot geometry. TWRP is the only intended recovery;
never generate, install or restore CM recovery. No phone operation or release
kernel selection is implied by building this independent experiment.
