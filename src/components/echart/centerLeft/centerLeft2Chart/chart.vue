<template>
  <div>
    <Echart
      id="centreLeft2Chart"
      ref="centreLeft2ChartRef"
      :options="options"
      height="360px"
      width="330px"
    ></Echart>
  </div>
</template>

<script>
import Echart from '@/common/echart';
export default {
  data() {
    return {
      options: {},
    };
  },
  components: {
    Echart,
  },
  props: {
    cdata: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    cdata: {
      handler(newData) {
        // 设置点的位置(经纬度)
        const geoCoordMap = {

        };
        let seriesData = [
          {
            name: '武侯区',
          },
          {
            name: '自贡市',
          },
          {
            name: '攀枝花市',
          },
          {
            name: '武侯区',
          },
          {
            name: '成华区',
          },
          {
            name: '龙泉驿区',
          },
          {
            name: '三明市',
          },
          {
            name: '南平市',
          },
          {
            name: '宁德市',
          },
        ];
        let convertData = function (data) {
          let scatterData = [];
          for (var i = 0; i < data.length; i++) {
            var geoCoord = geoCoordMap[data[i].name];
            if (geoCoord) {
              scatterData.push({
                name: data[i].name,
                value: geoCoord.concat(data[i].value),
              });
            }
          }
          return scatterData;
        };
        this.options = {
          showLegendSymbol: true,
          tooltip: {
            trigger: 'item',
            textStyle: {
              fontSize: 14,
              lineHeight: 22,
            },
            position: point => {
              // 固定在顶部
              return [point[0] + 50, point[1] - 20];
            },
            // 如果需要自定义 tooltip样式，需要使用formatter
            /*
              formatter: params => {
                return `<div style=""> ... </div>`
              }
            */
          },
          visualMap: {
            min: 0,
            max: 10,
            show: false,
            seriesIndex: 0,
            // 颜色
            inRange: {
              color: ['rgba(41,166,206, .5)', 'rgba(69,117,245, .9)'],
            },
          },
          // 底部背景
          geo: {
            show: true,
            aspectScale: 0.85, //长宽比
            zoom: 1.1,
            top: '10%',
            left: '9.5%',
            map: '成都',
            roam: false,
            itemStyle: {
              normal: {
                areaColor: 'rgba(0,0,0,0)',
                shadowColor: 'rgba(7,114,204, .8)',
                shadowOffsetX: 5,
                shadowOffsetY: 5,
              },
              emphasis: {
                areaColor: '#00aeef',
              },
            },
          },
          series: [
            {
              name: '传感器数量',
              type: 'map',
              aspectScale: 0.85, //长宽比
              zoom: 1.2,
              mapType: '成都', // 自定义扩展图表类型
              top: '10%',
              left: '9.5%',
              itemStyle: {
                normal: {
                  color: 'red',
                  areaColor: 'rgba(19,54,162, .5)',
                  borderColor: 'rgba(0,242,252,.3)',
                  borderWidth: 1,
                  shadowBlur: 7,
                  shadowColor: '#00f2fc',
                },
                emphasis: {
                  areaColor: '#4f7fff',
                  borderColor: 'rgba(0,242,252,.6)',
                  borderWidth: 2,
                  shadowBlur: 10,
                  shadowColor: '#00f2fc',
                },
              },
              label: {
                formatter: params => `${params.name}`,
                show: false,
                position: 'insideRight',
                textStyle: {
                  fontSize: 14,
                  color: '#efefef',
                },
                emphasis: {
                  textStyle: {
                    color: '#fff',
                  },
                },
              },
              data: newData,
            },
            {
              type: 'effectScatter',
              coordinateSystem: 'geo',
              symbolSize: 7,
              effectType: 'ripple',
              legendHoverLink: false,
              showEffectOn: 'render',
              rippleEffect: {
                period: 4,
                scale: 2.5,
                brushType: 'stroke',
              },
              zlevel: 1,
              itemStyle: {
                normal: {
                  color: '#99FBFE',
                  shadowBlur: 5,
                  shadowColor: '#fff',
                },
              },
              data: convertData(seriesData),
            },
          ],
        };
        // 重新选择区域
        this.handleMapRandomSelect();
      },
      immediate: true,
      deep: true,
    },
  },
  methods: {
    // 开启定时器
    startInterval() {
      const _self = this;
      // 应通过接口获取配置时间，暂时写死5s
      const time = 2000;
      if (this.intervalId !== null) {
        clearInterval(this.intervalId);
      }
      this.intervalId = setInterval(() => {
        _self.reSelectMapRandomArea();
      }, time);
    },
    // 重新随机选中地图区域
    reSelectMapRandomArea() {
      const length = 9;
      this.$nextTick(() => {
        try {
          const map = this.$refs.centreLeft2ChartRef.chart;
          let index = Math.floor(Math.random() * length);
          while (index === this.preSelectMapIndex || index >= length) {
            index = Math.floor(Math.random() * length);
          }
          map.dispatchAction({
            type: 'mapUnSelect',
            seriesIndex: 0,
            dataIndex: this.preSelectMapIndex,
          });
          map.dispatchAction({
            type: 'showTip',
            seriesIndex: 0,
            dataIndex: index,
          });
          map.dispatchAction({
            type: 'mapSelect',
            seriesIndex: 0,
            dataIndex: index,
          });
          this.preSelectMapIndex = index;
        } catch (error) {
          console.log(error)
        }
      });
    },
    handleMapRandomSelect() {
      this.$nextTick(() => {
        try {
          const map = this.$refs.centreLeft2ChartRef.chart;
          const _self = this;
          setTimeout(() => {
            _self.reSelectMapRandomArea();
          }, 0);
          // 移入区域，清除定时器、取消之前选中并选中当前
          map.on('mouseover', function (params) {
            clearInterval(_self.intervalId);
            map.dispatchAction({
              type: 'mapUnSelect',
              seriesIndex: 0,
              dataIndex: _self.preSelectMapIndex,
            });
            map.dispatchAction({
              type: 'mapSelect',
              seriesIndex: 0,
              dataIndex: params.dataIndex,
            });
            _self.preSelectMapIndex = params.dataIndex;
          });
          // 移出区域重新随机选中地图区域，并开启定时器
          map.on('globalout', function () {
            _self.reSelectMapRandomArea();
            _self.startInterval();
          });
          this.startInterval();
        } catch (error) {
          console.log(error)
        }
      });
    },
  },
};
</script>
