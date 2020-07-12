# cesium 加载 geojon 数据画边界线

> GeoJSON 是一种对各种地理数据结构进行编码的格式，基于 Javascript 对象表示法的地理空间信息数据交换格式。GeoJSON 对象可以表示几何、特征或者特征集合。

## 搜集的相关资料

- [AshKyd](https://github.com/AshKyd)的全球各国 geojson 边界数据 | [github 地址](https://github.com/AshKyd/geojson-regions.git) [网址](https://geojson-maps.ash.ms/)
- 支持鼠标拾取位置生成 json 数据文件 [geojson-map](http://geojson.io/#map=5/43.723/120.981)
- 全球部分国家边界 shp 数据下载 [OpenStreetMapDataExtracts](http://download.geofabrik.de/)
- HIGHCHARTS 提供的地图数据集 [Highmaps 地图数据集](https://img.hcharts.cn/mapdata/)

## 相关 cesium api

涉及的 cesium 相关 api [GeoJsonDataSource](http://cesium.xin/cesium/cn/Documentation1.62/GeoJsonDataSource.html?classFilter=GeoJsonDataSource)

## demo 代码

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <!-- Tell IE to use the latest, best version. -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <!-- Make the application on mobile take up the full browser screen and disable user scaling. -->
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no"
    />
    <title>Hello World!</title>
    <script src="../Cesium/Cesium.js"></script>
    <style>
      @import url(../Cesium/Widgets/widgets.css);
      html,
      body,
      #cesiumContainer {
        width: 100%;
        height: 100%;
        margin: 0;
        padding: 0;
        overflow: hidden;
      }
    </style>
  </head>

  <body>
    <div id="cesiumContainer"></div>
    <script>
      Cesium.Ion.defaultAccessToken = 'defaultAccessToken '

      var viewer = new Cesium.Viewer('cesiumContainer')
      viewer.dataSources.add(
        Cesium.GeoJsonDataSource.load('./CHN.geojson', {
          stroke: Cesium.Color.YELLOW.withAlpha(1),
          strokeWidth: 6.0,
          fill: Cesium.Color.RED.withAlpha(0)
        })
      )
    </script>
  </body>
</html>
```
