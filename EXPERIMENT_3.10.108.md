# CM12.1 MS330 Linux3.10.108 experiment

Independent experiment from merged baseline181521c9d2be347eb4cc3ad93e565cc5eaf74363.
Official kernel.org3.10.49/3.10.108 archives matched published SHA256 and exact
upstream Git trees4cd35b33/a56d0696. Apply their delta to the vendor tree with
an explicit3.10.49 three-way base; do not replace K7/Qualcomm hardware sources.
All75 conflicting files were reviewed. Per-file decisions are recorded in
experiment-resolution-decisions.json. Reference snapshot commits are local
synthetic imports of exact upstream trees; they do not impersonate upstream
commit identities. Unmodified release archive hashes/upstream tag identities
are recorded in the workspace audit/security/cm12.1/stable-3.10.108-experiment.

Build uses the exact working MS330 config (no enabled-option differences after
olddefconfig), Trusty/GCC4.8 and a separate output directory. Only ARM32 MS330
is build-validated; other architectures are not qualified. Security patch
level unchanged. Source merge/build success does not establish hardware or
complete security coverage. No phone flashing or ROM source selection made.

The original custom_kernel_src and qualified cm12/kernel/lge/m1-custom source
remain separate and unchanged. This folder can be discarded or refined without
losing the hardware-qualified baseline.

Build adaptation: LG scheduler diagnostics now use printk_deferred, the stable
replacement for printk_sched. Both original failed-build logs are preserved.
Full zImage and 17 modules compile; module vermagic and imported symbol CRCs
match. Hardware validation is pending. No default branch/source selection change.
