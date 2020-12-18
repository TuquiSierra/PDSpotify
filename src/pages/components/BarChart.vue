<template>
  <bar type="bar" :height="height" :series="[{ data: series }]" :options="chartOptions"></bar>
</template>
<script>
import ApexCharts from "vue-apexcharts";
export default {
  name: "BarChart",
  components: {
    bar: ApexCharts,
  },
  props: {
    labs: Array,
    series: Array,
    height:String,
  },
  data() {
    return {
      chartOptions: {
        series: [
          {
            data: this.series,
          },
        ],
        chart: {
          type: "bar",
          toolbar:{
              show:false,
          }
        },
        plotOptions: {
          bar: {
            horizontal: true,
            distributed: true,
          },
        },
        dataLabels: {
          enabled: true,
          formatter: function (val, opt) {
            return opt.w.globals.labels[opt.dataPointIndex];
          },
        },
        colors: [ "#28a15a","","#95a128", "#a14c28"],
        xaxis: {
          categories: this.labs,
        },
        yaxis: {
          labels: {
            show: false,
          },
        },
        legend:{
            show:false
        },
        tooltip:{
            x:{
                show:false,
            },
            y:{
                title:{
                    formatter:function(){
                        return ''
                    }
                }
            }
        }
      },
    };
  },
};
</script>
<style>
</style>