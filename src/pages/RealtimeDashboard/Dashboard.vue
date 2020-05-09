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
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
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
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
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
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
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
                    "Precipitation  " +
                    params.value +
                    (params.seriesData.length
                      ? "：" + params.seriesData[0].data
                      : "")
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
     
      //for(let i = 20 ; i > 0 ; i--) {
       // d.push(date);
       // d[c].setDate(d[c].getDate() - 1);
        // eslint-disable-next-line no-console
       // console.log(i+" ")
            // eslint-disable-next-line no-console
        //console.log(d[c].getFullYear()+"-"+this.appendLeadingZeroes(d[c].getMonth()+1)+"-"+this.appendLeadingZeroes(d[c].getDate())+"T00:00:00Z");
       //var temp = d[c].getFullYear()+"-"+this.appendLeadingZeroes(d[c].getMonth()+1)+"-"+this.appendLeadingZeroes(d[c].getDate())+"T00:00:00Z"
       
       // c++
        await AxiosAPI.get("/sensors")
          //await HTTP.get(`get/customer/${1}`)
          .then(res => {
            // eslint-disable-next-line no-console
            //console.log(res.data);
            
            
            for (var i=res.data.length-1;i>=0;i--){

            // eslint-disable-next-line no-console
            console.log(res.data[i].temperature)
            this.line1.series[0].data.push(res.data[i].temperature)
            this.line2.series[0].data.push(res.data[i].humidity)
            this.line3.series[0].data.push(res.data[i].soilmoisture)
            this.line4.series[0].data.push(res.data[i].light)
            // eslint-disable-next-line no-console
            //console.log(new date(res.data[i].created_at+"+07:00"))

            var aestTime = new Date(res.data[i].created_at).toLocaleString("th-TH", {timeZone: "Asia/Bangkok"});
            // eslint-disable-next-line no-console
            console.log('Thai time: '+ new Date(aestTime))
            //new date(res.data[i].created_at+"+07:00")
            //new Date(aestTime)
            let d = new Date(aestTime);
            let date = d.getHours()+":"+this.setMinutesthis(d.getMinutes())
            this.line1.xAxis[0].data.push(date)
            this.line2.xAxis[0].data.push(date)
            this.line3.xAxis[0].data.push(date)
            this.line4.xAxis[0].data.push(date)
            }
            // eslint-disable-next-line no-console
            //console.log(this.line1.xAxis[0].data)
            // eslint-disable-next-line no-console
            //console.log(this.line1.series[0].data)
           
            // eslint-disable-next-line no-console
            
            //this.caseVisit = res.data.result
          })
          .catch(e => {
            // eslint-disable-next-line no-console
            console.log(e);
         });
      //}
      
      
    },
    // eslint-disable-next-line no-unused-vars
    setMinutesthis(m) {
      if(m<10){
        return "0"+m
      }
      return m
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
