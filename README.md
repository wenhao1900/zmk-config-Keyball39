# Keyball39 — DYA 20 分钟深度休眠

基于卖家 tangbonze/zmk-config-Keyball39 的 dya 分支迁移，来源提交 `d3be5907875c8e68db9041c34e175b03f02ff1c2`。

- 硬件：nice!nano、右手轨迹球、OLED；右手为中央，左手为外设。
- 使用 cormoran/ZMK main+dya、Zephyr 4.1、DYA PMW3610 驱动与 Studio 模块。
- 左右手均启用深度休眠：电池供电、20 分钟无操作后进入；USB 供电时不深睡。
- 按键矩阵启用 wakeup-source，深睡后按键唤醒。
- 保留本仓库的七层键位、静态组合键及宏；轨迹球 CPI 保留 1400，自动鼠标层默认关闭。
- 第 5 层为滚动，第 6 层为精细移动，使用卖家的 DYA 输入处理器。

## 首次迁移刷机

从旧 ZMK v0.3 迁移到 DYA 时，按照卖家要求，左右手分别先刷重置固件，再刷各自的新固件。重置会清除蓝牙配对和 Studio 保存的键位，需要重新配对；仓库内的自定义键位已保留。

双击复位键进入 UF2 磁盘，把对应文件拖入。完成迁移后，拔掉左右手 USB，以电池供电静置超过 20 分钟，再按左右手按键检查唤醒。

右手 USB 连接后，可打开 https://studio.dya.cormoran.works/ 调整休眠等设置。网页保存的设置可能覆盖固件默认值，测试前核对休眠超时为 20 分钟。

## 构建

```sh
make init-standalone
make build-all
```

GitHub Actions 会编译左右手与重置固件，并核对编译后的休眠时间及按键唤醒配置。
