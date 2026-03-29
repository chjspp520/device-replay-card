# DeviceReplayCard 项目简介

- DeviceReplayCard 是一个专为 Home Assistant 平台设计的自定义 Lovelace 卡片组件，用于可视化智能家居设备的活动历史和实时状态。该组件通过交互式时间线和楼层平面图，帮助用户回顾设备（如灯具、插座、传感器等）的运行记录，支持回放功能以模拟设备在特定日期的激活过程。
主要功能

- 事件回放与时间线：加载指定日期的设备历史数据（从 Home Assistant 的历史 API 获取），在时间线上显示设备激活段，支持播放/暂停、速度调节（1x-30x）和手动拖拽。支持过滤最小持续时间的事件，避免显示短暂活动。

- 平面图可视化：在自定义背景图像上叠加设备图标或圆点，根据事件时间点动态高亮活跃设备。支持设备位置、旋转、缩放和分层配置。

- 传感器数据集成：显示传感器（如温度、湿度）的历史值，在平面图上实时更新当前时间点的读数，支持自定义单位、颜色和位置。

- 日期与实时模式：内置日期选择器和日历弹出，支持前后切换日期。当选择当天时，提供实时更新，包括进行中事件的动态条和当前时间指示器。

- 自定义配置：通过 YAML 支持丰富的选项，如房间颜色、设备标签对齐、背景偏移/缩放、最小事件过滤（单位：秒）、预设速度等。兼容多种实体类型（开关、传感器等），并处理跨午夜事件。

- 适用场景
适用于智能家居用户，特别是需要分析设备使用模式、能源消耗或日常活动的场景。例如，查看空调/灯光的运行时长、传感器读数变化，或调试自动化规则。该组件强调用户友好性，支持移动端响应，并优化了性能

## 截图

以下是 DeviceReplayCard 的两个运行效果示例（左：基本视图；中：带事件提示视图 ； 右：gif动画演示）：

<div style="display: flex;justify-content: space-between;align-items: center;gap: 3px;">
  <img src="https://raw.githubusercontent.com/chjspp520/ha-device-replay-card/main/image.png" style="width: 20%; height: auto;" />
  <img src="https://raw.githubusercontent.com/chjspp520/ha-device-replay-card/main/2.png"style="width: 22%; height: auto;" />
  <img src="https://github.com/chjspp520/ha-device-replay-card/blob/main/ha-device-replay-card.gif?raw=true" style="width: 40%; height: auto;" />
</div>

## 配置示例

以下是 `device-replay-card` 的 YAML 配置示例。你可以复制并调整到你的 Home Assistant Lovelace 中。

```yaml
    type: custom:device-replay-card
    theme: input_select.theme
    dark_light_theme: dark,light
    api_base_url: http://192.168.1.62:5000/replay/api
    card_width: 400
    floorplan_height: 410
    background_image: /local/house/3d_ui2/关灯.png
    background_left: 0
    background_top: 0
    background_scale: 100
    device_label_align: right
    device_track_height: 8
    device_track_font-size: 10
    energy:
      entities:
        - entity: sensor.quan_wu_ri_yong_dian_liang
          name: 日用电
          x: 10
          "y": 290
          color: "#000000"
          sensor_background_color: rgba(0, 123, 255, 0.8)
          unit: kWh
        - entity: sensor.quanwu_zongglv
          name: 功 率
          x: 10
          "y": 330
          color: "#ffffff"
          sensor_background_color: rgba(34, 197, 94, 0.8)
          unit: W
    rooms:
      客厅: "#ea5506"
      主卧: "#47885e"
      次卧: "#008899"
      儿童房: "#0095d9"
      餐厅: "#eb6ea5"
      厨房: "#006e54"
      大卫生间: "#65318e"
      小卫生间: "#a86965"
    entities:
      - entity: switch.zimi_cn_1069218961_dhkg01_on_p_2_1
        name: 客厅-玄关灯
        room: 客厅
        image_url: /local/house/3d_ui2/玄关on.png
        x: 0
        "y": 0
        image_scale: 100
        rotation: 0
        layer: 1
        color: "#ea5506"
        on_state: "on"
      - entity: climate.lumi_cn_875402794_mcn02
        name: 客厅-空调
        room: 客厅
        image_url: /local/house/3d_ui2/空调.png
        x: 260
        "y": 300
        rotation: 90
        image_scale: 15
        layer: 2
        color: "#17b978"
        on_states:
          - cool
          - dry
          - fan_only
          - heat
  
```


