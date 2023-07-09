<template>
  <div id="centerRight2">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span>
          <icon name="align-left" class="text-icon"></icon>
        </span>
        <span class="fs-xl text mx-2">传感器区域数量</span>
      </div>
      <div class="d-flex ai-center flex-column body-box">
        <dv-capsule-chart class="dv-cap-chart" :config="config" />
<!--        <centerRight2Chart1 />-->
      </div>
    </div>
  </div>
</template>

<script>
// import centerRight2Chart1 from '@/components/echart/centerRight/centerRightChart'

export default {
  data() {
    return {
      config: {
        data: [
          {
            name: '武侯区',
            value: 4
          },
          {
            name: '双流区',
            value: 0
          },
          {
            name: '成华区',
            value: 0
          },
          {
            name: '锦江区',
            value: 0
          },
          {
            name: '郫都区',
            value: 0
          },
          {
            name: '温江区',
            value: 0
          },
          {
            name: '青羊区',
            value: 0
          },
          {
            name: '金牛区',
            value: 0
          },
          {
            name: '新都区',
            value: 0
          },
          {
            name: '龙泉驿区',
            value: 0
          },
          {
            name: '新津区',
            value: 0
          },
        ]
      }
    }
  },
  // components: { centerRight2Chart1 }
}
</script>

<style lang="scss" scoped>
#centerRight2 {
  $box-height: 410px;
  $box-width: 340px;
  padding: 5px;
  height: $box-height;
  width: $box-width;
  border-radius: 5px;
  .bg-color-black {
    padding: 5px;
    height: $box-height;
    width: $box-width;
    border-radius: 10px;
  }
  .text {
    color: #c3cbde;
  }
  .body-box {
    border-radius: 10px;
    overflow: hidden;
    .dv-cap-chart {
      width: 100%;
      height: 370px;
    }
  }
}
</style>
