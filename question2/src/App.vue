<template>
  <div id="app">
    <apexchart height="350" type="candlestick" :options="options" :series="series"></apexchart>
  </div>
</template>

<script>
import dayjs from 'dayjs'
import data_sample from './data/candle_data_sample'

export default {
  name: 'App',
  created() {
    const chartData = data_sample.map(record => ({
      x: dayjs(record.date).toDate(),
      y: [record.open, record.high, record.low, record.close]
    }))
    this.series = [
      {
        name: 'candle',
        data: chartData
      }
    ]
  },
  data() {
    return {
      series: [],
      options: {
        chart: {
          type: "candlestick",
          height: 350
        },
        title: {
          text: "CandleStick Chart",
          align: "left"
        },
        xaxis: {
          type: "datetime"
        },
        yaxis: {
          tooltip: {
            enabled: true
          }
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
