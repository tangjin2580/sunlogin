# Sunlogin

本插件可将贝锐向日葵的设备接入HomeAssistant，理论上支持所有插座。

## 已支持型号
- C1
- C1-2
- C1Pro
- C1Pro-BLE
- C2
- C2-BLE
- C4（单插孔计电量版）
- C4-V2（计电量版）
- P1
- P1Pro
- P2
- P4
- P8
- P8Pro

## 安装

### 方法 1：手动安装

1. 下载插件并将 `custom_components/sunlogin` 文件夹复制到 Home Assistant 根目录下的 `custom_components` 文件夹

### 方法 2：通过 HACS 安装

如果你已经安装了 [HACS](https://www.hacs.xyz/docs/use/download/download/)，可以点击下面的按钮快速添加：

[![通过HACS添加集成](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=tangjin2580&repository=sunlogin&category=integration)

或者，手动添加：

1. 点击右上角的 `Custom repositories`
2. 在弹出的窗口中输入以下信息：
   - **Repository**: `https://github.com/tangjin2580/sunlogin`
   - **Type**: `Integration`

## 添加集成

进入 `设置` > `设备与服务` > `添加集成`，并搜索 `sunlogin`

或者，点击下面的按钮直接添加集成：

[![添加集成](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start?domain=sunlogin)

## 关于本仓库

本仓库为 `tangjin2580/sunlogin`，在原始 `cx3Y/sunlogin` 基础上做了以下调整：

- **支持 C4 / C4-V2**：单插孔计电量版插座（信号串 `C4` 即覆盖 C4 与 C4-V2），接入后生成 1 个插座开关 + 功率/电压/电流/时·日·周·月·上月电量统计实体，行为等同 C2。
- **省流量**：默认 `electric_update`（电量轮询）与 `power_consumes_update`（能耗统计轮询）已关闭，仅保留状态轮询；远程（云）轮询间隔建议设为 300s（设置 → 设备与服务 → sunlogin → 配置）。远程开关为命令推送，与轮询频率无关，调大间隔不影响操控。
- **修复 entity_id 告警**：型号中的大写字母与连字符（如 `C4-V2`、`P8Pro`）会被清洗为合法 slug（`c4_v2`、`p8pro`），消除 HA 的 `invalid entity ID` 告警。

> 如需恢复电量轮询，把 `sunlogin.py` 中 `async_electric_update` / `async_power_consumes_update` 开头的提前 `return` 守卫去掉即可。
