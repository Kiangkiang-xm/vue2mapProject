<template>
  <div class="map-container" style="width: 100%; height: 600px;">
    <div id="map" style="width: 100%; height: 100%;"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import chinaMapData from "@/assets/map/china.json"; // 引入 china.json 文件

export default {
  name: "HelloWorld",
  data() {
    return {
      dataList: [
        { name: "南海诸岛", value: 0 },
        { name: "北京", value: 100 },
        { name: "天津", value: 200 },
        { name: "上海", value: 300 },
        { name: "重庆", value: 400 },
        { name: "河北", value: 500 },
        { name: "河南", value: 600 },
        { name: "云南", value: 700 },
        { name: "辽宁", value: 800 },
        { name: "黑龙江", value: 900 },
        { name: "湖南", value: 1000 },
        { name: "安徽", value: 1100 },
        { name: "山东", value: 1200 },
        { name: "新疆", value: 1300 },
        { name: "江苏", value: 1400 },
        { name: "浙江", value: 1500 },
        { name: "江西", value: 1600 },
        { name: "湖北", value: 1700 },
        { name: "广西", value: 1800 },
        { name: "甘肃", value: 1900 },
        { name: "山西", value: 2000 },
        { name: "内蒙古", value: 2100 },
        { name: "陕西", value: 2200 },
        { name: "吉林", value: 2300 },
        { name: "福建", value: 2400 },
        { name: "贵州", value: 2500 },
        { name: "广东", value: 2600 },
        { name: "青海", value: 2700 },
        { name: "西藏", value: 2800 },
        { name: "四川", value: 2900 },
        { name: "宁夏", value: 3000 },
        { name: "海南", value: 3100 },
        { name: "台湾", value: 3200 },
        { name: "香港", value: 3300 },
        { name: "澳门", value: 3400 },
      ],
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      // 注册地图
      echarts.registerMap("china", chinaMapData);

      // 初始化 ECharts 实例
      const myChart = echarts.init(document.getElementById("map"));

      // 地图配置
      const option = {
        tooltip: {
          formatter: (params) => {
            return `${params.seriesName}<br/>${params.name}：${params.value}`;
          },
        },
        visualMap: {
          min: 0,
          max: 3500,
          left: "left",
          top: "bottom",
          text: ["高", "低"],
          inRange: {
            color: ["#e0ffff", "blue"],
          },
          show: true,
        },
        geo: {
          map: "china",
          roam: false,
          zoom: 1,
          label: {
            normal: {
              show: true,
              fontSize: "10",
              color: "rgba(0,0,0,0.7)",
            },
          },
          itemStyle: {
            normal: {
              borderColor: "rgba(0, 0, 0, 0.2)",
            },
            emphasis: {
              areaColor: "skyblue",
              shadowOffsetX: 0,
              shadowOffsetY: 0,
              shadowBlur: 20,
              borderWidth: 0,
              shadowColor: "rgba(0, 0, 0, 0.5)",
            },
          },
        },
        series: [
          {
            name: "省份",
            type: "map",
            geoIndex: 0,
            data: this.dataList,
          },
        ],
      };

      // 设置地图数据
      myChart.setOption(option);
    },
  },
};
</script>

<style scoped>
.map-container {
  margin: auto;
}
</style>