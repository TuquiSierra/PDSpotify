<template>
  <div>
    <select v-model="weekIndex1">
      <option v-for="(d, index) in getDates" :key="d" :value="index">
        {{ d }}
      </option>
    </select>
    <select v-model="weekIndex2">
      <option v-for="(d, index) in getDates" :key="d" :value="index">
        {{ d }}
      </option>
    </select>
    <div id="chart">
      <apexchart
        type="radar"
        height="450px"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </div>
  </div>
</template>

<script>
import ApexCharts from "vue-apexcharts";
import clustering from "@/assets/clustering.json";
import data from "@/assets/radar-data.json";

export default {
  name: "RadarChart",
  components: {
    apexchart: ApexCharts,
  },
  data() {
    return {
      data: data,
      weekIndex1: 0,
      weekIndex2: 1,
    };
  },
  computed: {
    getDates() {
      var dates = [];
      clustering.forEach((c) => {
        dates.push(c.date);
      });
      return dates;
    },
    series() {
      var serie1_values = [];
      var serie2_values = [];
      data.forEach((d) => {
        serie1_values.push(d.weeks[this.weekIndex1]);
        serie2_values.push(d.weeks[this.weekIndex2]);
      });
      return [
        {
          name: "Semana 1",
          data: serie1_values,
        },
        {
          name: "Semana 2",
          data: serie2_values,
        },
      ];
    },
    chartOptions() {
      var others = [];
      data.forEach((d) => {
        others.push(d.name);
      });
      return {
        chart: {
          toolbar: {
            show: false,
          },
          type: "radar",
        },
        xaxis: {
          categories: others,
        },
        colors: ["#28a15a", "#a14c28"],
        yaxis: {
          show: false,
          max: 1,
        },
      };
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
