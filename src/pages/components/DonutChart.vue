<template>
      <donut type="donut" :series="percents" :options="chartOptions"></donut>
</template>
<script>
import ApexCharts from "vue-apexcharts";
export default {
  name: "DonutChart",
  components: {
    donut: ApexCharts,
  },
  props: {
      labs:Array,
      percents:Array,
  },
  data() {
    return {
      chartOptions: {
        chart: {
          type: "donut",
        },
        dataLabels: {
          enabled: true,
          formatter: function (val) {
            return val + "%";
          },
        },
        legend:{
          position:'bottom',
        },
        labels: this.labs,

        colors: ["#95a128","#b0afaf", "#28a15a", "#a14c28"],
      },
    };
  },
};
</script>
<style>
</style>