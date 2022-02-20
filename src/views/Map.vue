<template>
  <div class="about">
    <img src="./diymap.svg" alt="" style="width: 500px; height: auto" />
    <div id="map" class="map-contain"></div>
  </div>
</template>
<script>
import * as echarts from "echarts";
// import WorldData from "world-map-geojson";
// import china from "./diymap.svg";
import * as $ from "jquery";
export default {
  data() {
    return {
      // src: china,
      options: {
        title: {
          text: "Visit Route",
          left: "center",
          bottom: 10,
        },
        tooltip: {},
        geo: {
          map: "MacOdrum-LV5-floorplan-web",
          roam: true,
          emphasis: {
            itemStyle: {
              color: undefined,
            },
            label: {
              show: false,
            },
          },
        },
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
            polyline: true,
            lineStyle: {
              color: "#c46e54",
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
                  [110.6189462165178, 456.64349563895087],
                  [124.10988522879458, 450.8570048730469],
                  [123.9272226116071, 389.9520693708147],
                  [61.58708083147317, 386.87942320312504],
                  [61.58708083147317, 72.8954315876116],
                  [258.29514854771196, 72.8954315876116],
                  [260.75457021484374, 336.8559607533482],
                  [280.5277985253906, 410.2406672084263],
                  [275.948185765904, 528.0254369698661],
                  [111.06907909458701, 552.795792593471],
                  [118.87138231445309, 701.365737015904],
                  [221.36468155133926, 758.7870354617745],
                  [307.86195445452006, 742.164737297712],
                  [366.8489324762834, 560.9895157073103],
                  [492.8750778390066, 560.9895157073103],
                  [492.8750778390066, 827.9639780566406],
                  [294.9255269587053, 827.9639780566406],
                  [282.79803391043527, 868.2476088113839],
                ],
              },
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
      var ROOT_PATH = "/img/diymap.a1be8d4f.svg";

      var chartDom = document.getElementById("map");
      var myChart = echarts.init(chartDom);
      var option;

      $.get(ROOT_PATH, function (svg) {
        echarts.registerMap("Beef_cuts_France", { svg: svg });
        option = {
          tooltip: {},
          visualMap: {
            left: "center",
            bottom: "10%",
            min: 5,
            max: 100,
            orient: "horizontal",
            text: ["", "Price"],
            realtime: true,
            calculable: true,
            inRange: {
              color: ["#dbac00", "#db6e00", "#cf0000"],
            },
          },
          series: [
            {
              name: "French Beef Cuts",
              type: "map",
              map: "Beef_cuts_France",
              roam: true,
              emphasis: {
                label: {
                  show: false,
                },
              },
              selectedMode: false,
              data: [
                { name: "Queue", value: 15 },
                { name: "Langue", value: 35 },
                { name: "Plat de joue", value: 15 },
                { name: "Gros bout de poitrine", value: 25 },
                { name: "Jumeau à pot-au-feu", value: 45 },
                { name: "Onglet", value: 85 },
                { name: "Plat de tranche", value: 25 },
                { name: "Araignée", value: 15 },
                { name: "Gîte à la noix", value: 55 },
                { name: "Bavette d'aloyau", value: 25 },
                { name: "Tende de tranche", value: 65 },
                { name: "Rond de gîte", value: 45 },
                { name: "Bavettede de flanchet", value: 85 },
                { name: "Flanchet", value: 35 },
                { name: "Hampe", value: 75 },
                { name: "Plat de côtes", value: 65 },
                { name: "Tendron Milieu de poitrine", value: 65 },
                { name: "Macreuse à pot-au-feu", value: 85 },
                { name: "Rumsteck", value: 75 },
                { name: "Faux-filet", value: 65 },
                { name: "Côtes Entrecôtes", value: 55 },
                { name: "Basses côtes", value: 45 },
                { name: "Collier", value: 85 },
                { name: "Jumeau à biftek", value: 15 },
                { name: "Paleron", value: 65 },
                { name: "Macreuse à bifteck", value: 45 },
                { name: "Gîte", value: 85 },
                { name: "Aiguillette baronne", value: 65 },
                { name: "Filet", value: 95 },
              ],
            },
          ],
        };
        myChart.setOption(option);
      });

      option && myChart.setOption(option);
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
