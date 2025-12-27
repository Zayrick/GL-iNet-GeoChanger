# GL iNet 路由器更改区域指南

本教程旨在指导用户如何在不同型号的 GL iNet 路由器上更改区域设置。请注意，此操作涉及直接写入闪存，存在一定风险。操作前请确保充分理解每一步骤，并小心谨慎地执行。

## 风险警告
- 直接写入闪存可能导致设备无法启动。
- 请在操作前仔细阅读教程，确保操作步骤无误。
- 操作过程中，请谨慎执行每一步。

## 准备工作
在开始之前，请确保您已经备份了路由器的重要数据。更改区域设置前，建议查看当前的分区信息以确认写入的位置。您可以在路由器已安装的 OpenWRT 系统中使用以下命令查看分区信息：

```bash
lsblk
# 或
fdisk -l
```

## 更改区域操作步骤
### MT3600BE路由器

1. **更改区域设置**：
   MT3000 路由器的区域设置信息存储在 `/dev/mtdblock3`。以下命令将区域代码 "US" 写入该分区的指定位置。`bs=1` 指定块大小为 1 字节，`seek=16520` 指定从偏移量 16520开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以使更改生效。dd if=/dev/mtdblock3 bs=1 count=8 skip=16520 2>/dev/null | hexdump -C用于查看是否更改
   ```bash
   dd if=/dev/mtdblock3 bs=1 count=8 skip=16520 2>/dev/null | hexdump -C
   echo -n "US" | dd of=/dev/mtdblock3 bs=1 seek=16520 conv=notrunc 2>&1
   sync
   dd if=/dev/mtdblock3 bs=1 count=8 skip=16520 2>/dev/null | hexdump -C
   reboot
   ```
### MT3000 路由器

1. **更改区域设置**：
   MT3000 路由器的区域设置信息存储在 `/dev/mtdblock3`。以下命令将区域代码 "US" 写入该分区的指定位置。`bs=1` 指定块大小为 1 字节，`seek=136` 指定从偏移量 136 开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以使更改生效。
   ```bash
   echo "US" | dd of=/dev/mtdblock3 bs=1 seek=136
   sync
   reboot
   ```

### MT2500 路由器

1. **解除写保护并更改区域设置**：
   MT2500 路由器的区域设置信息存储在 `/dev/mmcblk0boot1`。首先，解除该分区的写保护，然后将区域代码 "US" 写入指定位置。`bs=1` 指定块大小为 1 字节，`seek=136` 指定从偏移量 136 开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以应用更改。
   ```bash
   echo 0 > /sys/block/mmcblk0boot1/force_ro
   echo "US" | dd of=/dev/mmcblk0boot1 bs=1 seek=136
   sync
   reboot
   ```

### AX1800/AXT1800 路由器

1. **更改区域设置**：
   AX1800/AXT1800 路由器的区域设置信息存储在 `/dev/mtdblock8`。以下命令将区域代码 "US" 写入该分区的指定位置。`bs=1` 指定块大小为 1 字节，`seek=152` 指定从偏移量 152 开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以使更改生效。
   ```bash
   echo "US" | dd of=/dev/mtdblock8 bs=1 seek=152
   sync
   reboot
   ```

### MT6000 路由器

1. **更改区域设置**：
   MT6000 路由器的区域设置信息存储在 `/dev/mmcblk0p2`。以下命令将区域代码 "US" 写入该分区的指定位置，`conv=notrunc` 确保不会截断现有数据。`bs=1` 指定块大小为 1 字节，`seek=136` 指定从偏移量 136 开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以使更改生效。
   ```bash
   echo "US" | dd of=/dev/mmcblk0p2 conv=notrunc bs=1 seek=136
   sync
   reboot
   ```
   
### BE3600 路由器

1. **更改区域设置**：
   BE3600 路由器的区域设置信息存储在 `/dev/mtdblock11`。以下命令将区域代码 "US" 写入该分区的指定位置，`conv=notrunc` 确保不会截断现有数据。`bs=1` 指定块大小为 1 字节，`seek=136` 指定从偏移量 136 开始写入数据。`sync` 确保所有写入操作已完成，`reboot` 重新启动设备以使更改生效。
   ```bash
   hexdump -C -n 512 /dev/mtdblock11 # 确认输出包含 CN 字样
   echo -n "US" |dd of=/dev/mtdblock11 conv=notrunc bs=1 seek=136
   sync
   reboot
   ```

## 重置固件
成功更改区域后，建议重置固件以确保所有设置正确应用。重置操作可以通过路由器的管理界面执行。

## 语言切换
若要查看某些特定区域的特定功能，请将系统语言从简体中文切换到繁体中文。可通过替换 `/www/i18n` 目录下的相应文件实现。

- 将文件名后缀为 `zh-cn` 的文件替换为 `zh-tw` 文件。

通过以上步骤，您可以在 GL iNet 路由器上成功更改区域设置。再次提醒，请在操作过程中保持高度警觉，以避免不必要的设备故障。
