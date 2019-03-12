<template>
  <div>
    <div id="chart1" style="width:100%;height:500px"></div>
  </div>
</template>

<script>
import {GoogleCharts} from 'google-charts';
export default {
  data(){
    return{
      info:[]
    }
  },
  mounted(){
    GoogleCharts.load(this.drawChart,{
      'packages': ['corechart']
    });
  },
  methods:{
    drawChart(){
      this.$axios.get("http://localhost:5000").then(response=>{
        this.info=response.data
        const data = GoogleCharts.api.visualization.arrayToDataTable(response.data);
        const pie_1_chart = new GoogleCharts.api.visualization.LineChart(document.getElementById('chart1'));
        const pie_1_options = {
          chart: {
            title: 'Box Office Earnings in First Two Weeks of Opening',
            subtitle: 'in millions of dollars (USD)'
          },
          width: 900,
          height: 500
        };
        pie_1_chart.draw(data,pie_1_options);
      })
      
    }
  }
}
</script>

<style>
</style>
