# Natural Earth Vector - 快速參考指南 / Quick Reference Guide

## 🌍 項目簡介 / Project Overview

**Natural Earth Vector** 是一個公共領域的地理數據集，提供三種精度的全球矢量地圖數據。  
**Natural Earth Vector** is a public domain geographic dataset providing global vector map data at three resolutions.

- **網站 / Website**: http://naturalearthdata.com
- **版本 / Version**: 5.2.0-pre
- **授權 / License**: 公共領域 / Public Domain

## 📊 數據比例尺 / Data Scales

| 比例尺 / Scale | 用途 / Use Case | 文件大小 / File Size |
|---------------|----------------|---------------------|
| 1:10m | 高精度地圖、區域地圖 / High detail, regional maps | 大 / Large |
| 1:50m | 中精度地圖、國家地圖 / Medium detail, country maps | 中 / Medium |
| 1:110m | 低精度地圖、全球地圖 / Low detail, world maps | 小 / Small |

## 📁 主要數據類別 / Main Data Categories

### 文化數據 / Cultural Data
- ✅ 國家邊界 / Country boundaries (admin_0)
- ✅ 行政區劃 / Administrative divisions (admin_1)
- ✅ 城市和居住地 / Cities and populated places
- ✅ 道路和鐵路 / Roads and railroads
- ✅ 機場和港口 / Airports and ports

### 物理數據 / Physical Data
- ✅ 海岸線 / Coastlines
- ✅ 河流和湖泊 / Rivers and lakes
- ✅ 陸地和海洋 / Land and ocean
- ✅ 地理標籤區域 / Geographic regions
- ✅ 經緯網 / Graticules

## 🔧 支持的格式 / Supported Formats

| 格式 / Format | 擴展名 / Extension | 用途 / Purpose |
|--------------|-------------------|---------------|
| Shapefile | .shp, .dbf, .shx, .prj | GIS 標準格式 / GIS standard |
| SQLite | .sqlite | 單文件數據庫 / Single-file database |
| GeoPackage | .gpkg | 現代 GIS 標準 / Modern GIS standard |
| GeoJSON | .geojson | Web 應用 / Web applications |

## 🚀 快速開始 / Quick Start

### 下載數據 / Download Data
```bash
# 克隆倉庫 / Clone repository
git clone https://github.com/nvkelso/natural-earth-vector.git

# 或從官網下載打包文件 / Or download packages from website
# http://naturalearthdata.com/downloads
```

### 構建數據 / Build Data
```bash
# 安裝依賴 / Install dependencies (需要 GDAL)
# Ubuntu/Debian
sudo apt-get install gdal-bin python3-gdal

# macOS
brew install gdal

# 構建所有包 / Build all packages
make all

# 僅構建 zip 文件 / Build only zip files
make zip

# 僅構建 SQLite / Build only SQLite
make zips/packages/natural_earth_vector.sqlite.zip
```

### 使用 Docker / Using Docker
```bash
# 構建 Docker 鏡像 / Build Docker image
docker build -t natural-earth .

# 運行構建 / Run build
docker run -v $(pwd):/data natural-earth make all
```

## 💡 常見用例 / Common Use Cases

### 1. 在 QGIS 中使用 / Use in QGIS
```
1. 打開 QGIS / Open QGIS
2. 圖層 → 添加圖層 → 添加矢量圖層 / Layer → Add Layer → Add Vector Layer
3. 選擇 .shp 文件 / Select .shp files
4. 添加到地圖 / Add to map
```

### 2. 在 Python 中使用 / Use in Python
```python
import geopandas as gpd

# 讀取 Shapefile / Read Shapefile
world = gpd.read_file('10m_cultural/ne_10m_admin_0_countries.shp')

# 繪製地圖 / Plot map
world.plot(figsize=(15, 10))

# 篩選數據 / Filter data
asia = world[world['CONTINENT'] == 'Asia']
```

### 3. 在 JavaScript 中使用 / Use in JavaScript
```javascript
// 使用 Mapbox GL JS / Using Mapbox GL JS
map.addSource('countries', {
    type: 'vector',
    url: 'path/to/natural-earth-vector.geojson'
});

map.addLayer({
    id: 'countries-layer',
    type: 'fill',
    source: 'countries',
    paint: {
        'fill-color': '#088',
        'fill-opacity': 0.8
    }
});
```

## ⚙️ 主要構建目標 / Main Build Targets

| 目標 / Target | 描述 / Description | 耗時 / Duration |
|--------------|-------------------|----------------|
| `make zip` | 創建所有 zip 包 / Create all zip packages | ~30-45 分鐘 / mins |
| `make sqlite` | 創建 SQLite 數據庫 / Create SQLite database | ~15-20 分鐘 / mins |
| `make gpkg` | 創建 GeoPackage / Create GeoPackage | ~15-20 分鐘 / mins |
| `make geojson` | 轉換為 GeoJSON / Convert to GeoJSON | ~20-30 分鐘 / mins |

## 🔍 重要文件 / Important Files

| 文件 / File | 說明 / Description |
|------------|-------------------|
| `README.md` | 項目說明 / Project README |
| `CHANGELOG` | 變更記錄 / Change history |
| `VERSION` | 當前版本 / Current version |
| `Makefile` | 構建腳本 / Build script |
| `UPDATE_PROCEDURE.md` | 更新流程 / Update procedure |
| `LICENSE.md` | 授權信息 / License information |

## 📈 項目優勢 / Project Strengths

- ✅ **高質量數據** / High-quality data
- ✅ **公共領域** / Public domain
- ✅ **多比例尺** / Multiple scales
- ✅ **精心製作** / Carefully crafted
- ✅ **定期更新** / Regular updates
- ✅ **豐富屬性** / Rich attributes
- ✅ **多格式支持** / Multiple formats

## ⚠️ 常見問題 / Common Issues

### 問題 1：構建失敗 / Build Fails
```bash
# 檢查 GDAL 安裝 / Check GDAL installation
ogr2ogr --version

# 安裝缺失依賴 / Install missing dependencies
pip install -r requirements.txt  # (需創建此文件 / needs to be created)
```

### 問題 2：內存不足 / Out of Memory
```bash
# 單獨構建各個比例尺 / Build scales separately
make zips/110m_cultural/110m_cultural.zip  # 先構建小文件 / Build small files first
make zips/50m_cultural/50m_cultural.zip
make zips/10m_cultural/10m_cultural.zip
```

### 問題 3：權限錯誤 / Permission Errors
```bash
# 使用 sudo 或更改文件權限 / Use sudo or change permissions
sudo make all
# 或 / or
chmod -R 755 .
```

## 🎯 推薦改進（基於分析）/ Recommended Improvements

### 優先級 1 / Priority 1 (立即實施 / Immediate)
1. ⚡ 添加 `requirements.txt` / Add requirements.txt
2. ⚡ 創建自動化測試 / Create automated tests  
3. ⚡ 改進 Docker 配置 / Improve Docker setup

### 優先級 2 / Priority 2 (短期 / Short-term)
4. 📦 模塊化 Makefile / Modularize Makefile
5. 🔄 遷移到 GitHub Actions / Migrate to GitHub Actions
6. 📚 添加多語言文檔 / Add multi-language docs

### 優先級 3 / Priority 3 (長期 / Long-term)
7. 🌐 開發 Web API / Develop Web API
8. 📊 數據質量監控 / Data quality monitoring
9. 🤖 自動化更新流程 / Automated update pipeline

## 📚 學習資源 / Learning Resources

### 官方資源 / Official Resources
- 📖 官網文檔 / Official Documentation: http://naturalearthdata.com
- 📂 GitHub 倉庫 / GitHub Repository: https://github.com/nvkelso/natural-earth-vector
- 📝 更新流程 / Update Procedure: See `UPDATE_PROCEDURE.md`

### 工具文檔 / Tool Documentation
- 🗺️ GDAL/OGR: https://gdal.org/
- 📦 GeoPackage: https://www.geopackage.org/
- 🌐 GeoJSON: https://geojson.org/

### 教程 / Tutorials
- QGIS 教程 / QGIS Tutorials: https://www.qgis.org/en/docs/
- GeoPandas 指南 / GeoPandas Guide: https://geopandas.org/
- Mapbox GL JS 文檔 / Mapbox GL JS Docs: https://docs.mapbox.com/

## 🤝 如何貢獻 / How to Contribute

```bash
# 1. Fork 倉庫 / Fork the repository
# 2. 克隆你的 Fork / Clone your fork
git clone https://github.com/YOUR_USERNAME/natural-earth-vector.git

# 3. 創建功能分支 / Create feature branch
git checkout -b feature/your-feature-name

# 4. 進行修改 / Make changes
# 5. 提交修改 / Commit changes
git commit -m "Description of changes"

# 6. 推送到你的 Fork / Push to your fork
git push origin feature/your-feature-name

# 7. 創建 Pull Request / Create Pull Request
```

## 📞 聯繫方式 / Contact

- **維護者 / Maintainer**: Nathaniel V. KELSO (@nvkelso)
- **組織 / Organization**: NACIS (North American Cartographic Information Society)
- **問題報告 / Issue Tracker**: https://github.com/nvkelso/natural-earth-vector/issues

## 📑 相關文檔 / Related Documentation

詳細分析請參閱 / For detailed analysis, see:
- 📄 **中文完整分析** / Chinese Full Analysis: `SYSTEM_ANALYSIS_ZH.md`
- 📄 **English Full Analysis**: `SYSTEM_ANALYSIS_EN.md`

---

**最後更新 / Last Updated**: 2026-02-01  
**版本 / Version**: 1.0
