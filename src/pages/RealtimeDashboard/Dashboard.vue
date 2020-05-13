<template>
  <div class="dashboard-page">
    <h1 class="page-title">Dashboard</h1>
    <b-row>
      <b-col lg="12" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Temperature" close>
            <echart :options="line1" :init-options="initEchartsOptions" style="height: 370px"></echart>
          
          </Widget>
        </div>
      </b-col>
      <b-col lg="12" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Humidity" close>
            <echart :options="line2" :init-options="initEchartsOptions" style="height: 370px"></echart>
         
          </Widget>
        </div>
      </b-col>
      <b-col lg="12" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Soilmoisture" close>
            <echart :options="line3" :init-options="initEchartsOptions" style="height: 370px"></echart>
           
          </Widget>
        </div>
      </b-col>
      <b-col lg="12" sm="6" xs="12">
        <div class="pb-xlg h-100">
          <Widget class="h-100 mb-0" title="Ligth Intensity" close>
            <echart :options="line4" :init-options="initEchartsOptions" style="height: 370px"></echart>
         
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
    echart: ECharts
  },
  data() {
    return {
      mock,
      initEchartsOptions: {
        renderer: "canvas"
      },
      line1: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross"
          }
        },

        grid: {
          top: 70,
          bottom: 50
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1]
              }
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Date: " +
                    params.value +
                    (params.seriesData.length
                      ? ", Value: " + params.seriesData[0].data: "")
                  );
                }
              }
            },
            data: [
              
            ]
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor
            },
            axisLine: {
              lineStyle: {
                color: axisColor
              }
            }
          }
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [
              
            ]
          }
        ]
      },
      line2: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross"
          }
        },

        grid: {
          top: 70,
          bottom: 50
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1]
              }
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Date: " +
                    params.value +
                    (params.seriesData.length
                      ? ", Value: " + params.seriesData[0].data: "")
                  );
                }
              }
            },
            data: [
            ]
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor
            },
            axisLine: {
              lineStyle: {
                color: axisColor
              }
            }
          }
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [
            ]
          }
        ]
      },
      line3: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross"
          }
        },

        grid: {
          top: 70,
          bottom: 50
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1]
              }
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Date: " +
                    params.value +
                    (params.seriesData.length
                      ? ", Value: " + params.seriesData[0].data: "")
                  );
                }
              }
            },
            data: [
            ]
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor
            },
            axisLine: {
              lineStyle: {
                color: axisColor
              }
            }
          }
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [
            ]
          }
        ]
      },
      line4: {
        color: lineColors,
        tooltip: {
          trigger: "none",
          axisPointer: {
            type: "cross"
          }
        },

        grid: {
          top: 70,
          bottom: 50
        },
        xAxis: [
          {
            type: "category",
            axisTick: {
              alignWithLabel: true
            },
            axisLine: {
              onZero: false,
              lineStyle: {
                color: lineColors[1]
              }
            },
            axisPointer: {
              label: {
                formatter: function(params) {
                  return (
                    "Date: " +
                    params.value +
                    (params.seriesData.length
                      ? ", Value: " + params.seriesData[0].data: "")
                  );
                }
              }
            },
            data: [
            ]
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: axisColor
            },
            axisLine: {
              lineStyle: {
                color: axisColor
              }
            }
          }
        ],
        series: [
          {
            name: "2016 Precipitation",
            type: "line",
            smooth: true,
            data: [
            ]
          }
        ]
      }
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
        await AxiosAPI.get("/sensors")
          //await HTTP.get(`get/customer/${1}`)
          .then(res => {
            // eslint-disable-next-line no-console  
            for (var i=res.data.length-1; i>=0 ;i--){
              // eslint-disable-next-line no-console
              this.line1.series[0].data.push(res.data[i].temperature)
              this.line2.series[0].data.push(res.data[i].humidity)
              this.line3.series[0].data.push(res.data[i].soilmoisture)
              this.line4.series[0].data.push(res.data[i].light)
              // eslint-disable-next-line no-console

              try {
                var dateUTCString = new Date(res.data[i].created_at).toUTCString();
              } catch (error) {
                console.log("error to parsing time" + error)
              }

              // convert to string date to Date obj
              let d = new Date(dateUTCString)

              // format time to show in graph
              var dateStringFormat = d.getDate() + '/' + d.getMonth() + '/' + d.getFullYear() + ' ' + d.getHours() + ":" + this.setMinutesthis(d.getMinutes())

              // push the data to x-axis
              this.line1.xAxis[0].data.push(dateStringFormat)
              this.line2.xAxis[0].data.push(dateStringFormat)
              this.line3.xAxis[0].data.push(dateStringFormat)
              this.line4.xAxis[0].data.push(dateStringFormat)
            }
          })
          .catch(e => {
            // eslint-disable-next-line no-console
            console.log(e);
         });     
    },
    // eslint-disable-next-line no-unused-vars
    setMinutesthis(m) {
      if(m<10){
        return "0"+m
      }
      return m
    },
    getRevenueData() {
      const data = [];
      const seriesCount = 3;
      const accessories = ["SMX", "Direct", "Networks"];

      for (let i = 0; i < seriesCount; i += 1) {
        data.push({
          label: accessories[i],
          data: Math.floor(Math.random() * 100) + 1
        });
      }

      return data;
    },
    appendLeadingZeroes(n) {
      if(n <= 9){
        return "0" + n;
      }
      return n
}
  },
  computed: {
    donut() {
      let revenueData = this.getRevenueData();
      let { danger, info, primary } = this.appConfig.colors;
      let series = [
        {
          name: "Revenue",
          data: revenueData.map(s => {
            return {
              name: s.label,
              y: s.data
            };
          })
        }
      ];
      return {
        chart: {
          type: "pie",
          height: 120
        },
        credits: {
          enabled: false
        },
        title: false,
        plotOptions: {
          pie: {
            dataLabels: {
              enabled: false
            },
            borderColor: null,
            showInLegend: true,
            innerSize: 60,
            size: 100,
            states: {
              hover: {
                halo: {
                  size: 1
                }
              }
            }
          }
        },
        colors: [danger, info, primary],
        legend: {
          align: "right",
          verticalAlign: "middle",
          layout: "vertical",
          itemStyle: {
            color: "#495057",
            fontWeight: 100,
            fontFamily: "Montserrat"
          },
          itemMarginBottom: 5,
          symbolRadius: 0
        },
        exporting: {
          enabled: false
        },
        series
      };
    }
  }
};
</script>

<style src="./Dashboard.scss" lang="scss" />
