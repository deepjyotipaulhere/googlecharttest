<template>
  <div>
    <div id="chart1" style="width:100%;height:500px">
      <GChart
        :settings="{packages:['bar']}"
        :data="chartData"
        :options="chartOptions"
        :createChart="(el, google) => new google.charts.Bar(el)"
        @ready="onChartReady"
       />
    </div>
  </div>
</template>

<script>
import {GChart} from 'vue-google-charts';
export default {
  data(){
    return{
      info:[],
      chartData:[]
    }
  },
  components:{
    GChart
  },
  mounted(){
    this.drawChart()
  },
  methods:{
    drawChart(){
      this.$axios.get("http://localhost:5000").then(response=>{
        this.chartData=response.data
      })
    },
    onChartReady (chart, google) {
      this.chartsLib = google
    }
  },
  computed: {
    chartOptions () {
      if (!this.chartsLib) return null
      return this.chartsLib.charts.Bar.convertOptions({
        chart: {
          title: 'Company Performance',
          subtitle: 'Sales, Expenses, and Profit: 2014-2017'
        },
        bars: 'horizontal', // Required for Material Bar Charts.
        hAxis: { format: 'decimal' },
        height: 400,
        colors: ['#1b9e77', '#d95f02', '#7570b3']
      })
    }
  },
}
</script>

<style>
</style>
