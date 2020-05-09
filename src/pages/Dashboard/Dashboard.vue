<template>
  <div class="dashboard-page">
    <h1 class="page-title">Dashboard</h1>
    <b-row>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Temperature Now (Celsius)" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-3">
                <strong>{{ TempNow }}</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Humidity Now (%RH)" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-3">
                <strong>{{ HumidNow }}</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Soilmoisture Now (%)" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-3">
                <strong>{{ SoilNow }}</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Ligth Intensity Now (Lux)" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-3">
                <strong>{{ LightNow }}</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
    </b-row>

    <!-- ส่วนกราฟ -->
    <b-row>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Temperature (Celsius)" close>
            <echart
              :options="line1"
              :init-options="initEchartsOptions"
              style="height: 370px"
            ></echart>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Humidity (%RH)" close>
            <echart
              :options="line2"
              :init-options="initEchartsOptions"
              style="height: 370px"
            ></echart>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Soilmoisture (%)" close>
            <echart
              :options="line3"
              :init-options="initEchartsOptions"
              style="height: 370px"
            ></echart>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Ligth Intensity (Lux)" close>
            <echart
              :options="line4"
              :init-options="initEchartsOptions"
              style="height: 370px"
            ></echart>
          </Widget>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col xs="12" lg="6" xl="4"></b-col>
    </b-row>
    <b-row>
      <b-col lg="6">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Set Threshold" close>
            <div class="w-80 p-3">
              <span>Light Intensity</span>
              <b-form-input v-model="lightthreshold" placeholder></b-form-input>
            </div>

            <div class="w-80 p-3">
              <span>Soil Moisture</span>
              <b-form-input
                v-model="soilmoisturethreshold"
                placeholder
              ></b-form-input>
            </div>
            <div class="w-80 p-3">
              <b-button variant="info" @click="clickSetthreshold()"
                >Submit</b-button
              >
            </div>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3">
        <div class="pb-xlg h-100">
          <Widget class="h-70 mb-0" title="Light Intensity Threshold" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-1">
                <strong>{{ lightthreshold2 }} Lux</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
      <b-col lg="3">
        <div class="pb-xlg h-100">
          <Widget class="h-70 mb-0" title="Soil Moisture Threshold" close>
            <div class="w-80 p-3 text-center">
              <h1 class="display-1">
                <strong>{{ soilmoisturethreshold2 }} %</strong>
              </h1>
            </div>
          </Widget>
        </div>
      </b-col>
    </b-row>
  </div>
</template>

<script>
 /* eslint-disable */
import Widget from "@/components/Widget/Widget";
import BigStat from "./components/BigStat/BigStat";
import mock from "./mock";

import ECharts from "vue-echarts/components/ECharts";
import "echarts/lib/chart/line";
import "echarts/lib/chart/themeRiver";
import "echarts/lib/component/tooltip";
import "echarts/lib/component/legend";

import { Chart } from "highcharts-vue";

import config from "../../config";

const colors = config.app.colors;
const { primary, warning, success } = colors;
const chartColors = config.app.chartColors;
const { axisColor } = chartColors;
import axios from "axios";
const AxiosAPI = axios.create({
  baseURL: "https://api.inwza.club",
  timeout: 1000,
  headers: { "Content-Type": "application/json" },
});

let lineColors = [primary, success, warning];

export default {
  name: "Dashboard",
  components: {
    Widget,
    BigStat,
    highcharts: Chart,
    echart: ECharts,
  },
  data() {
    return {
      mock,
      initEchartsOptions: {
        renderer: "canvas",
      },
      lightthreshold: "",
      soilmoisturethreshold: "",
      lightthreshold2: "",
      soilmoisturethreshold2: "",
      TempNow: "",
      HumidNow: "",
      SoilNow: "",
      LightNow: "",



      line1: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross",
          },
        },

        grid: {
          top: 70,
          bottom: 50,
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true,
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1],
              },
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
                  );
                },
              },
            },
            data: [],
          },
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor,
            },
            axisLine: {
              lineStyle: {
                color: axisColor,
              },
            },
          },
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [],
          },
        ],
      },
      line2: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross",
          },
        },

        grid: {
          top: 70,
          bottom: 50,
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true,
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1],
              },
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
                  );
                },
              },
            },
            data: [],
          },
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor,
            },
            axisLine: {
              lineStyle: {
                color: axisColor,
              },
            },
          },
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [],
          },
        ],
      },
      line3: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross",
          },
        },

        grid: {
          top: 70,
          bottom: 50,
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true,
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1],
              },
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
                  );
                },
              },
            },
            data: [],
          },
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor,
            },
            axisLine: {
              lineStyle: {
                color: axisColor,
              },
            },
          },
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [],
          },
        ],
      },
      line4: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross",
          },
        },

        grid: {
          top: 70,
          bottom: 50,
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true,
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1],
              },
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
                  );
                },
              },
            },
            data: [],
          },
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor,
            },
            axisLine: {
              lineStyle: {
                color: axisColor,
              },
            },
          },
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [],
          },
        ],
      },
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      var d = [];
      var c = 0;

      for (let i = 14; i >= 0; i--) {
        d.push(new Date());
        d[c].setDate(d[c].getDate() - i);

        var temp =
          d[c].getFullYear() +
          "-" +
          this.appendLeadingZeroes(d[c].getMonth() + 1) +
          "-" +
          this.appendLeadingZeroes(d[c].getDate()) +
          "T00:00:00Z";
        let payload = {
          created_at: temp,
        };
        c++;
        await AxiosAPI.post("/sensors/date", payload)
          //await HTTP.get(`get/customer/${1}`)
          .then((res) => {
            var a = 0;
            var b = 0;
            var c = 0;
            var d = 0;
            for (var i = 0; i < res.data.length; i++) {
              a += res.data[i].temperature;
              b += res.data[i].humidity;
              c += res.data[i].soilmoisture;
              d += res.data[i].light;
            }

            // eslint-disable-next-line no-console
            console.log(a / res.data.length);
            this.line1.series[0].data.push(a / res.data.length);
            this.line2.series[0].data.push(b / res.data.length);
            this.line3.series[0].data.push(c / res.data.length);
            this.line4.series[0].data.push(d / res.data.length);
            // eslint-disable-next-line no-console
            console.log(temp.split("T")[0]);
            this.line1.xAxis[0].data.push(temp.split("T")[0]); //2020-05-08T00:00:00Z
            this.line2.xAxis[0].data.push(temp.split("T")[0]);
            this.line3.xAxis[0].data.push(temp.split("T")[0]);
            this.line4.xAxis[0].data.push(temp.split("T")[0]);
            //this.caseVisit = res.data.result
          })
          .catch((e) => {
            // eslint-disable-next-line no-console
            console.log(e);
          });
      }

      await AxiosAPI.get("/get/threshold")
        //await HTTP.get(`get/customer/${1}`)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log(res.data.lightthreshold);
          this.lightthreshold2 = res.data.lightthreshold;
          this.soilmoisturethreshold2 = res.data.soilmoisturethreshold;
        })
        .catch((e) => {
          // eslint-disable-next-line no-console
          console.log(e);
        });
      await AxiosAPI.get("/sensors")
      .then(res => {
        for (var i = res.data.length-1;i>=0;i--){
        console.log(res.data[i].temperature)
        this.TempNow = Number(res.data[0].temperature)
        this.HumidNow = Number(res.data[0].humidity)
        this.SoilNow = Number(res.data[0].soilmoisture)
        this.LightNow = Number(res.data[0].light)
        }
      })
      .catch((e) => {
        console.log(e);
      })
    },
    clickSetthreshold() {
      let payload = {
        lightthreshold: Number(this.lightthreshold),
        soilmoisturethreshold: Number(this.soilmoisturethreshold),
      };
      // eslint-disable-next-line no-console
      console.log(payload);
      AxiosAPI.post("/set/threshold", payload)
        //await HTTP.get(`get/customer/${1}`)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log(res);
          location.reload();
        })
        .catch((e) => {
          // eslint-disable-next-line no-console
          console.log(e);
        });
    },
    getRandomData() {
      const arr = [];

      for (let i = 0; i < 25; i += 1) {
        arr.push(Math.random().toFixed(1) * 10);
      }

      return arr;
    },
    getRevenueData() {
      const data = [];
      const seriesCount = 3;
      const accessories = ["SMX", "Direct", "Networks"];

      for (let i = 0; i < seriesCount; i += 1) {
        data.push({
          label: accessories[i],
          data: Math.floor(Math.random() * 100) + 1,
        });
      }

      return data;
    },
    appendLeadingZeroes(n) {
      if (n <= 9) {
        return "0" + n;
      }
      return n;
    },
  },
  computed: {
    donut() {
      let revenueData = this.getRevenueData();
      let { danger, info, primary } = this.appConfig.colors;
      let series = [
        {
          name: "Revenue",
          data: revenueData.map((s) => {
            return {
              name: s.label,
              y: s.data,
            };
          }),
        },
      ];
      return {
        chart: {
          type: "pie",
          height: 120,
        },
        credits: {
          enabled: false,
        },
        title: false,
        plotOptions: {
          pie: {
            dataLabels: {
              enabled: false,
            },
            borderColor: null,
            showInLegend: true,
            innerSize: 60,
            size: 100,
            states: {
              hover: {
                halo: {
                  size: 1,
                },
              },
            },
          },
        },
        colors: [danger, info, primary],
        legend: {
          align: "right",
          verticalAlign: "middle",
          layout: "vertical",
          itemStyle: {
            color: "#495057",
            fontWeight: 100,
            fontFamily: "Montserrat",
          },
          itemMarginBottom: 5,
          symbolRadius: 0,
        },
        exporting: {
          enabled: false,
        },
        series,
      };
    },
  },
};
</script>

<style src="./Dashboard.scss" lang="scss" />
