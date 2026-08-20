# 🛵 北京电瓶车充电站定位数据集

> 把北京每一辆电瓶车的"能量补给站"，装进你的代码里。
> 全量站点坐标 · 结构化字段 · 开箱即用

![GitHub stars](https://img.shields.io/badge/站点数-10%2C000%2B-blue) ![覆盖](https://img.shields.io/badge/覆盖-北京16区-green) ![格式](https://img.shields.io/badge/格式-CSV%2FJSON-orange) ![License](https://img.shields.io/badge/License-CC--BY--4.0-lightgrey) ![更新](https://img.shields.io/badge/最近更新-2026--08-brightgreen)

---

## 🚀 为什么要用这份数据

你不需要再费劲爬、不需要去别的平台翻、不需要处理脏坐标——**一个文件，全量充电站**：

| | 说明 |
|---|---|
| 📍 **全量站点** | 【站点数待核对】个充电站定位点，覆盖北京 16 个行政区 |
| 🎯 **坐标精准** | 经纬度已清洗对齐（GCJ-02 国测局坐标），可直接用于地图渲染 |
| 📦 **字段结构化** | 名称 / 地址 / 经纬度 / 充电口数量 / 运营商 / 状态 / 采集时间 一键可用 |
| 🔄 **持续更新** | 数据定期增量刷新，保留采集时间字段，便于做趋势分析 |
| 🆓 **免费开源** | CC-BY-4.0，商用也放心（署名即可） |

---

## 📦 数据内容

### 文件清单

```
beijing_charging_stations.csv      # 主数据（UTF-8，逗号分隔，带表头）
beijing_charging_stations.json     # 同数据 JSON 版（数组，键名见下）
sample/                            # 样例数据（前 100 条，供快速预览）
```

### 字段说明

| 字段 | 类型 | 说明 |
|---|---|---|
| `station_id` | string | 站点唯一 ID |
| `name` | string | 站点名称 |
| `address` | string | 详细地址 |
| `district` | string | 行政区（朝阳 / 海淀 / 丰台 …） |
| `lng` | float | 经度（GCJ-02） |
| `lat` | float | 纬度（GCJ-02） |
| `slot_count` | int | 充电口数量（无可查=0） |
| `operator` | string | 运营商 / 品牌 |
| `status` | string | 状态（正常 / 维护 / 未知） |
| `collected_at` | datetime | 采集时间 |

### 样例

```json
{
  "station_id": "BJ_000001",
  "name": "XX街道便民充电桩",
  "address": "北京市朝阳区XX路XX号",
  "district": "朝阳",
  "lng": 116.48329,
  "lat": 39.92324,
  "slot_count": 12,
  "operator": "XX科技",
  "status": "正常",
  "collected_at": "2026-08-01 10:00:00"
}
```

---

## 🛠 快速开始

### 1. 下载

```bash
# 直接下载 CSV
curl -L -O https://github.com/你的用户名/beijing-charging-stations/raw/main/beijing_charging_stations.csv
```

### 2. 用 Python 读（pandas）

```python
import pandas as pd

df = pd.read_csv("beijing_charging_stations.csv")
print(df.shape)          # (站点数, 10)
print(df["district"].value_counts())   # 各区分布
```

### 3. 30 秒画个分布图

```python
import matplotlib.pyplot as plt

df["district"].value_counts().plot.bar(figsize=(10, 4), title="北京充电站行政区分布")
plt.tight_layout(); plt.show()
```

---

## 📊 你能拿它做什么

- 🗺 **地图应用**：folium / leaflet / 高德地图直接渲染站点点位
- 🔋 **充电规划**：找"附近 500 米有没有桩"，做出行决策
- 🏢 **选址分析**：结合人口/小区数据，找充电服务盲区
- 📈 **趋势研究**：按 `collected_at` 看设施建设增长曲线
- 🧮 **教学示例**：坐标聚类（DBSCAN）、空间可视化最好的练手数据

---

## 🔍 数据来源与质量

- **采集方式**：【填写：公开地图 POI / 爬虫 / 数据合作】
- **清洗流程**：去重（同址合并）→ 坐标校验（范围/有效性过滤）→ 字段标准化
- **坐标系**：GCJ-02（国测局火星坐标，国内地图通用；如需 WGS-84 可自行转换，或 issue 留言批量提供）
- **采样说明**：站点为**动态数据**，充电桩可能新增/拆除，以 `collected_at` 为准

> ⚠️ **免责声明**：本数据仅供参考，非官方数据，可能存在滞后或遗漏。请勿用于涉及人身/财产安全的决策场景。数据版权归原始来源所有，本仓库仅做整理发布。

---

## 📜 License

[CC-BY-4.0](LICENSE) —— 你可以自由使用、修改、商用，**只需署名**。

如果你用这份数据做了有趣的东西，欢迎在 README 里挂出来 👀

---

## 🔖 更新日志

- `2026-08` v1.0：初版发布，全量站点坐标

---

<p align="center">⭐ 如果这份数据帮到了你，点个 Star 让更多人看到它 ⭐</p>
