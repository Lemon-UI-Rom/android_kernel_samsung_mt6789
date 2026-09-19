# Compatible With a24, a15, a16, gta9, gta9wifi 
(All Firmwares)






# Build Instructions

## 1. How to Build

### Option A: Build via GitHub Actions
1. Fork this repository to your own GitHub account.
2. Navigate to the Actions tab in your forked repository.
3. Select the build workflow from the left sidebar.
4. Click Run workflow.
5. Enter toolchain url or keep default one
6. Once the process completes, you can download the compiled kernel and boot image from the Artifacts section of the finished run. <br>
`Note: the default values does not require to clean before building, you may need to enable it if you did changes`

---

### Option B: Manual Build
### Get Toolchain
Get the proper toolchain packages from AOSP.

Please unzip the toolchain file in the path where `build_kernel.sh` is located:
- `kernel/prebuilts/`
- `kernel/prebuilts-master/`
- `prebuilts/`

### Set Build Environment and Export Target Config
```bash
cd kernel-5.10
python scripts/gen_build_config.py --kernel-defconfig a15_00_defconfig \
                                   --kernel-defconfig-overlays "entry_level.config" \
                                   -m user -o ../out/target/product/a15/obj/KERNEL_OBJ/build.config

export ARCH=arm64
export CROSS_COMPILE="aarch64-linux-gnu-"
export CROSS_COMPILE_COMPAT="arm-linux-gnueabi-"
export OUT_DIR="../out/target/product/a15/obj/KERNEL_OBJ"
export DIST_DIR="../out/target/product/a15/obj/KERNEL_OBJ"
export BUILD_CONFIG="../out/target/product/a15/obj/KERNEL_OBJ/build.config"
```

### To Build
```bash
- Place your boot image in the root
- Run ./build_kernel.sh to build the Kernel
- Run ./script/repack to repack the boot image with the new Kernel
```

## 2. Output Files
- **Kernel**: `out/target/product/a15/obj/KERNEL_OBJ/kernel-5.10/arch/arm64/boot/Image.gz`
- **Module**: `out/target/product/a15/obj/KERNEL_OBJ/*.ko`

## 3. How to Clean
```bash
./clean_build.sh
```
note: build_kernel.sh already cleans before building, so no need to do before building

## Acknowledgements
This project includes code from the https://github.com/ReeViiS69/sm155f/ project, licensed under the GPL-2.0. Also, a huge thanks to ReeViiS69 for helping me build the kernel.

This project includes code from the https://github.com/WildPlusKernel/kernel_patches/ project, licensed under the GPL-2.0.

This project includes code from the https://github.com/fei-ke/android_kernel_samsung_sm8550/ project, licensed under the GPL-2.0.

This project includes executable file/s from https://github.com/topjohnwu/Magisk/ project, licensed under the GPL-3.0.

This project includes file/s from https://android.googlesource.com/platform/external/avb project, licensed under the Apache License, Version 2.0.

This project includes patch from https://github.com/fatalcoder524.

**Donate to the original developer (poqdavid):**
<br/>**BTC Legacy:** 1Q2JQG3iCLZPT2iJfDLow1oQVGKmxheoAh
<br/>**BTC Segwit:** bc1q8gurls0wjkfe43ygmrqmu2pzmyjetnrvgws9sr
<br/>**BCH:** qrks52smlqw7d8700d77uqvmve03d4knzvd2vghaqz
<br/>**ETH:** 0x7218779242a8425879B09969431c20F5eC1a192D
