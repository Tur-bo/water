<!--
  描述：拖放地图组件，默认尺寸是 500 * 300
  接收属性参数：
    lat: 纬度
    lng: 经度
  自定义事件：
    drag: 拖放完成事件
  示例：
    <redmap @drag="dragMap" lat="22.574405" lng="114.095388"></redmap>
-->
<template>
  <div class="m-map">
    <div id="js-container" class="map"></div>
  </div>
</template>

<script>
import remoteLoad from '../../config/remoteLoad.js'
import { MapKey, MapCityName } from  '../../config/config'
export default {
  props: ['points','lng'],
  data () {
    return {
      searchKey: '',
      placeSearch: null,
      dragStatus: false,
      AMapUI: null,
      AMap: null
    }
  },
  watch: {
    
  },
  methods: {
    // 实例化地图
    initMap () {
      // 加载PositionPicker，loadUI的路径参数为模块名中 'ui/' 之后的部分
      let AMapUI = this.AMapUI = window.AMapUI
      let AMap = this.AMap = window.AMap
      AMapUI.loadUI(['misc/PositionPicker'], PositionPicker => {
        let mapConfig = {
          zoom: 9,
          cityName: MapCityName
        }
        console.log(this.points);
        if (this.lat && this.lng) {
          mapConfig.center = [this.lng, this.lat]
        }
        let infoWindow = new AMap.InfoWindow({
//            isCustom: true,
            offset: new AMap.Pixel(0, -30)
        });
        let map = new AMap.Map('js-container', mapConfig)
        // 加载地图搜索插件
        // AMap.service('AMap.PlaceSearch', () => {
        //   this.placeSearch = new AMap.PlaceSearch({
        //     pageSize: 5,
        //     pageIndex: 1,
        //     citylimit: true,
        //     city: MapCityName,
        //     map: map,
        //     panel: 'js-result'
        //   })
        // })
        // 启用工具条
        AMap.plugin(['AMap.ToolBar'], function () {
          map.addControl(new AMap.ToolBar({
            position: 'RB'
          }))
        })
        // 创建地图上的点
        for(var i=0;i< this.points.length;i++){
           console.log(this.points[i]);
           let marker = new AMap.Marker({
                position: [this.points[i].lng,this.points[i].lat],
                title: this.points.name,
                map: map,
                icon: this.points[i].icon,
            });
            marker.content = this.points[i].name + this.points[i].desc;
            marker.on('click', markerClick =>{
                infoWindow.setContent(markerClick.target.content);
                infoWindow.open(map, markerClick.target.getPosition());
            });
            // marker.emit('click', {target: marker});
        }

      })
    }
    
  },
  async created () {
    // 已载入高德地图API，则直接初始化地图
    if (window.AMap && window.AMapUI) {
      this.initMap()
    // 未载入高德地图API，则先载入API再初始化
    } else {
      await remoteLoad(`http://webapi.amap.com/maps?v=1.3&key=${MapKey}`)
      await remoteLoad('http://webapi.amap.com/ui/1.0/main.js')
      this.initMap()
    }
  }
}
</script>

<style lang="css">
.m-map{ position: relative; height:100%;top:0;left:0;right:0;bottom:0;width:100%;}
.m-map .map{ width: 100%; height: 100%; }
.m-map .search{ position: absolute; top: 10px; left: 10px; width: 285px; z-index: 1; }
.m-map .search input{ width: 180px; border: 1px solid #ccc; line-height: 20px; padding: 5px; outline: none; }
.m-map .search button{ line-height: 26px; background: #fff; border: 1px solid #ccc; width: 50px; text-align: center; }
.m-map .result{ max-height: 300px; overflow: auto; margin-top: 10px; }
</style>