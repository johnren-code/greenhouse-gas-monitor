<template>
  <div>
    <Chart :cdata="cdata" />
  </div>
</template>

<script>
import Chart from './chart.vue'
export default {
  data () {
    return {
      drawTiming: null,
      cdata: {
        year: null,
        weekCategory: [],
        radarData: [],
        radarDataAvg: [],
        maxData: 40,
        weekMaxData: [],
        weekLineData: [],
        humidityMaxData: 120,
        humidityData: []
      }
    }
  },
  components: {
    Chart,
  },
  mounted () {
    this.drawTimingFn();
  },
  beforeDestroy () {
    clearInterval(this.drawTiming);
  },
  methods: {
    drawTimingFn () {
      this.setData();
      this.drawTiming = setInterval(() => {
        this.setData();
      }, 6000);
    },
    setData () {
      // 清空轮询数据
      this.cdata.weekCategory = [
          '1:00',
          '2:00',
          '3:00',
          '4:00',
          '5:00',
          '6:00',
          '7:00',
          '8:00',
          '9:00',
          '10:00',
          '11:00',
          '12:00',
          '13:00',
          '14:00',
          '15:00',
          '16:00',
          '17:00',
          '18:00',
          '19:00',
          '20:00',
          '21:00',
          '22:00',
          '23:00',
          '24:00'
      ];
      this.cdata.humidityData = [
          102,
          102.6,
          103,
          103.3,
          103.5,
          103.9,
          104,
          104.4,
          103.8,
          103.8,
          102.9,
          103.8,
          99.6,
          100,
          97.4,
          100,
          101.3,
          101.7,
          102.9,
          104,
          105.2,
          105.3,
          106.1,
      ]
      this.cdata.weekMaxData = [];
      this.cdata.weekLineData = [
          23,
          22.8,
          22.8,
          22.7,
          22.5,
          22.3,
          22.3,
          22.2,
          22.9,
          23.8,
          25.5,
          27.3,
          30.4,
          30.8,
          30.3,
          28.7,
          28.4,
          28,
          27.2,
          25.8,
          25.2,
          24.6,
          24.3,
      ];
      // this.cdata.radarData = [
      //     1,
      //     2,
      //     3,
      //     4,
      //     5,
      //     6,
      //     7,
      // ];
      this.cdata.radarDataAvg = [];
      // let dateBase = new Date();
      // this.cdata.year = dateBase.getFullYear();
      // 周数据
      // for (let i = 0; i < 7; i++) {
      //   // 日期
      //   // let date = new Date();
      //   // this.cdata.weekCategory.unshift([date.getMonth() + 1, date.getDate()-i].join("/"));
      //
      //   // 折线图数据
      //   // this.cdata.weekMaxData.push(this.cdata.maxData);
      //   // let distance = Math.round(Math.random() * 11000 + 500);
      //   // this.cdata.weekLineData.push(distance);
      //
      //   // 雷达图数据
      //   // 我的指标
      //   // let averageSpeed = +(Math.random() * 5 + 3).toFixed(3);
      //   // let maxSpeed = averageSpeed + +(Math.random() * 3).toFixed(2);
      //   // let hour = +(distance / 1000 / averageSpeed).toFixed(1);
      //   // let radarDayData = [distance, averageSpeed, maxSpeed, hour];
      //   // this.cdata.radarData.unshift(radarDayData);
      //   //
      //   // // 平均指标
      //   // let distanceAvg = Math.round(Math.random() * 8000 + 4000);
      //   // let averageSpeedAvg = +(Math.random() * 4 + 4).toFixed(3);
      //   // let maxSpeedAvg = averageSpeedAvg + +(Math.random() * 2).toFixed(2);
      //   // let hourAvg = +(distance / 1000 / averageSpeed).toFixed(1);
      //   // let radarDayDataAvg = [
      //   //   distanceAvg,
      //   //   averageSpeedAvg,
      //   //   maxSpeedAvg,
      //   //   hourAvg
      //   // ];
      //   // this.cdata.radarDataAvg.unshift(radarDayDataAvg);
      // }

    }
  }
};
</script>

<style lang="scss" scoped>
</style>