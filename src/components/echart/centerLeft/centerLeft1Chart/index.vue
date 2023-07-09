<template>
  <div>
    <Chart :cdata="cdata" />
  </div>
</template>

<script>
import Chart from './chart.vue';
export default {
  data () {
    return {
      cdata: {
        xData: ["CO2传感器", "CH4传感器", "温湿度传感器"],
        seriesData: [
          { value: 25, name: "CO2传感器" },
          { value: 50, name: "CH4传感器" },
          { value: 25, name: "温湿度传感器" }
        ]
      }
    }
  },
  components: {
    Chart,
  },
  mounted () {
  },
  methods: {
  }
}
</script>

<style lang="scss" scoped>
</style>