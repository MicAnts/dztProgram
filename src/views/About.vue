<template>
  <div class="about">
    <div id="map" class="map-contain"></div>
  </div>
</template>
<script>
import * as echarts from "echarts";
import WorldData from "world-map-geojson";
// import WorldDataSvg from "../assets/2750411.svg";
export default {
  data() {
    return {
      options: {
        grid: {
          width: "100%",
          height: "100%",
          left: "0%",
          right: "0%",
          bottom: "0%",
          containLabel: true,
        },
        geo: [
          {
            map: "world",
            shwo: true,
            roam: true,
            aspectScale: 1,
            regions: [
              {
                name: "China",
                itemStyle: {
                  areaColor: "red",
                  color: "red",
                },
              },
            ],
          },
        ],
        series: [
          {
            name: "Route",
            type: "lines",
            coordinateSystem: "geo",
            geoIndex: 0,
            emphasis: {
              label: {
                show: true,
              },
            },
            polyline: false,
            smooth: true,
            lineStyle: {
              color: "#000",
              width: 5,
              opacity: 1,
              type: "solid",
              curveness: -0.2,
            },
            effect: {
              show: true,
              period: 8,
              color: "#a10000",
              constantSpeed: 80,
              trailLength: 0,
              symbolSize: [20, 12],
              symbol:
                "path://M35.5 40.5c0-22.16 17.84-40 40-40s40 17.84 40 40c0 1.6939-.1042 3.3626-.3067 5H35.8067c-.2025-1.6374-.3067-3.3061-.3067-5zm90.9621-2.6663c-.62-1.4856-.9621-3.1182-.9621-4.8337 0-6.925 5.575-12.5 12.5-12.5s12.5 5.575 12.5 12.5a12.685 12.685 0 0 1-.1529 1.9691l.9537.5506-15.6454 27.0986-.1554-.0897V65.5h-28.7285c-7.318 9.1548-18.587 15-31.2715 15s-23.9535-5.8452-31.2715-15H15.5v-2.8059l-.0937.0437-8.8727-19.0274C2.912 41.5258.5 37.5549.5 33c0-6.925 5.575-12.5 12.5-12.5S25.5 26.075 25.5 33c0 .9035-.0949 1.784-.2753 2.6321L29.8262 45.5h92.2098z",
            },
            data: [
              {
                coords: [
                  [100, 30],
                  [-100, 40],
                ],
              },
            ],
            markPoint: {
              symbol: "pin",
              data: [
                {
                  name: "China",
                  value: "China",
                  coord: [100, 30],
                },
                {
                  name: "Sudan",
                  value: "Sudan",
                  coord: [30, 10],
                },
                {
                  name: "United States",
                  value: "老美",
                  coord: [-100, 40],
                },
              ],
            },
          },
          {
            type: "effectScatter",
            coordinateSystem: "geo",
            geoIndex: 0,
            symbolSize: function (params) {
              return (params[2] / 100) * 15 + 5;
            },
            itemStyle: {
              color: "#b02a02",
            },
            encode: {
              tooltip: 2,
            },
            data: [
              [10, 10, 10],
              [10, 20, 10],
              [30, 10, 20],
              [-30, 10, 3],
            ],
          },
        ],
      },
    };
  },
  created() {},
  mounted() {
    // this.options.series.data = WorldData;
    this.$nextTick(() => {
      this.initMap();
    });
  },
  methods: {
    initMap() {
      console.log(WorldData);
      WorldData.features.forEach((element) => {
        if (element.properties.name === "China") {
          console.log(element);
          return false;
        }
      });
      echarts.registerMap("world", {
        geoJson: WorldData,
      });
      const myEcharts = echarts.init(document.getElementById("map"));

      myEcharts.setOption(this.options);
    },
  },
};
</script>
<style lang="less" scoped>
.map-contain {
  width: 800px;
  height: 500px;
  margin: 0 auto;
  border: 1px solid #efefef;
}
</style>
