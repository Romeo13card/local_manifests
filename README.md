# Shared local manifest: fog and xun, LineageOS 24.0

Both devices are defined in one file, `manifest.xml`, on the `lineage-24.0` branch.
The same manifest is maintained in `Xun-Development/local_manifests` and
`decoder-dev/local_manifests`. Xun projects and shared dependencies are hosted in
Xun-Development; the fog device/vendor/prebuilt and its separate Dolby stack remain in decoder-dev.

For a fresh LineageOS checkout:

```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs
git clone https://github.com/Romeo13card/local_manifests -b lineage-24.0 .repo/local_manifests
repo sync -c -j8 --no-clone-bundle --no-tags
source build/envsetup.sh
breakfast xun
m bacon
```

Use `breakfast fog` to select fog. Existing checkouts can update this local-manifest
repository on `lineage-24.0`; Git removes the former three XML files as part of that update.
All overrides below are pinned. The main LineageOS platform still follows its configured upstream branch.

## Published project revisions

| Project | Repository | Branch | Revision |
|---|---|---|---|
| `device/xiaomi/fog` | [decoder-dev/device_xiaomi_fog](https://github.com/decoder-dev/device_xiaomi_fog/tree/fog-fixes) | `fog-fixes` | `4347bbd4ccfae85228c406829f0c82b1efd94e33` |
| `vendor/xiaomi/fog` | [decoder-dev/vendor_xiaomi_fog](https://github.com/decoder-dev/vendor_xiaomi_fog/tree/fog-fixes) | `fog-fixes` | `93f5caf5e2d743d4c5eff5e2af13e2e0e0c9def7` |
| `device/xiaomi/fog-kernel` | [decoder-dev/device_xiaomi_fog-kernel](https://github.com/decoder-dev/device_xiaomi_fog-kernel/tree/fog-fixes) | `fog-fixes` | `d12c019a3f5ef426972bdcb045cfa42cfb1625b5` |
| `hardware/dolby` | [decoder-dev/hardware_dolby](https://github.com/decoder-dev/hardware_dolby/tree/fog-fixes) | `fog-fixes` | `b7c92b9e9e8005a5ef8ce8d0f5ef75d6f125aa9e` |


## Kernel sources

ROM builds use the two prebuilt-kernel repositories listed above. Their sources are
published separately:

- fog: [decoder-dev/kernel_xiaomi_sm6225](https://github.com/decoder-dev/kernel_xiaomi_sm6225/tree/Kuroha/BakaSU-update), `40473e02cfd9c155b55384ae58e41d18afec2650`.

See [AUDIT_XUN.md](AUDIT_XUN.md) for the xun findings, fixes and validation limits.
The fog stability OTA passed build/VINTF/archive/boot checks. The xun loader fixtures
and DolbyAtmos resource/Kotlin compilation passed. A full xun OTA and runtime on a
phone/tablet have not been tested by the builder; these checks do not establish that
all freezes or reboots are resolved.
