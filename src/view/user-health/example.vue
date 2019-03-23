<template>
    <div ref="dom"></div>
</template>

<script>
import echarts from 'echarts'
import { on, off } from '@/libs/tools'
export default {
  name: 'serviceRequests',
  data () {
    return {
      dom: null
    }
  },
  methods: {
    resize () {
      this.dom.resize()
    }
  },
  mounted () {
    const option = {
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'cross',
          label: {
            backgroundColor: '#6a7985'
          }
        }
      },
      grid: {
        top: '3%',
        left: '1.2%',
        right: '1%',
        bottom: '3%',
        containLabel: true
      },
      xAxis: [
        {
          type: 'category',
          boundaryGap: false,
          data: ['3.1', '3.2', '3.3', '3.4', '3.5', '3.6', '3.7']
        }
      ],
      yAxis: [
        {
          type: 'value'
        }
      ],
      series: [
        {
          name: '心率',
          type: 'line',
          areaStyle: {normal: {
            color: '#2d8cf0'
          }},
          data: [60, 56, 70, 64, 63, 59, 69]
        },
        {
          name: '体温',
          type: 'line',
          areaStyle: {normal: {
            color: '#10A6FF'
          }},
          data: [37.6, 37.5, 37.9, 36.9, 36.7, 37.8, 37.7]
        },
        {
          name: '车内温度',
          type: 'line',
          areaStyle: {normal: {
            color: '#0C17A6'
          }},
          data: [19.3, 22.1, 22.2, 19.6, 20.7, 20.4, 21.3]
        },
        {
          name: '户外气温',
          type: 'line',
          areaStyle: {normal: {
            color: '#4608A6'
          }},
          data: [10, 2, 8, 9, 7, 10, 9]
        },
      ]
    }
    this.$nextTick(() => {
      this.dom = echarts.init(this.$refs.dom)
      this.dom.setOption(option)
      on(window, 'resize', this.resize)
    })
  },
  beforeDestroy () {
    off(window, 'resize', this.resize)
  }
}
</script>
