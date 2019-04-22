<template>
  <div id="app">
    <!-- echarts容器 -->
    <div id="main" style="width: 600px;height:400px;" ref="echarts"></div>
  </div>
</template>
<script>
// 引入echarts
import echarts from "echarts";

export default {
  name: "app",
  //   元素出现了才能获取到dom元素
  data() {
    return {
          option:{
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'cross',
            crossStyle: {
                color: '#999'
            }
        }
    },
    toolbox: {
        feature: {
            dataView: {show: true, readOnly: false},
            // 设置什么形态的图
            magicType: {show: true, type: ['line', 'bar']},
            restore: {show: true},
            saveAsImage: {show: true}
        }
    },
    // 图代表的是啥
    legend: {
        data:['蒸发量','降水量','平均温度']
    },
    // x轴代表什么
    xAxis: [
        {
            type: 'category',
            data: ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月'],
            axisPointer: {
                type: 'shadow'
            }
        }
    ],
    // Y轴代表什么
    yAxis: [
        {
            type: 'value',
            name: '水量',
            min: 0,
            max: 250,
            interval: 50,
            axisLabel: {
                formatter: '{value} ml'
            }
        },
        {
            type: 'value',
            name: '温度',
            min: 0,
            max: 25,
            // 初始值
            interval: 5,
              // 单位
            axisLabel: {
                formatter: '{value} °C'
            }
        }
    ],
    series: [
        {
            name:'蒸发量',
            // stack:'堆叠',//堆叠柱状图在此设置成统一名称即可
            type:'bar',
            data:[2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3]
        },
        {
            name:'降水量',
            type:'bar',
            barGap: '-100%',
            data:[2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3]
        },
        {
            name:'平均温度',
            type:'line',
            yAxisIndex: 1,
            data:[2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
        }
    ]
},
    }
  },
  mounted() {
    // 获取dom元素,加上echarts效果
    //  var myChart = echarts.init(document.getElementById('main'));
    let myChart = echarts.init(this.$refs.echarts);
    // 指定图表的配置项和数据
    let weatherIcons = {
      Sunny: "./data/asset/img/weather/sunny_128.png",
      Cloudy: "./data/asset/img/weather/cloudy_128.png",
      Showers: "./data/asset/img/weather/showers_128.png"
    };
    let tpldata = [
    {
    Month: "1月,2月,3月,4月,5月,6月,7月,8月,8月,10月,11月,12月",
    zhengFaLiang:"2.0,4.9,7.0,23.2,25.6,76.7,135.6,162.2,32.6,20.0,6.4,3.3",
    jiangShuiLiang:"2.6,5.9,9.0,26.4,28.7,70.7,175.6,182.2,48.7,18.8,6.0,2.3",
    pingJunWenDu: "2.0,2.2,3.3,4.5,6.3,10.2,20.3,23.4,23.0,16.5,12.0,6.2"
    }
    ];
  
    // 月份
    this.option.xAxis[0].data=tpldata[0].Month.split(",");
   
    // Math.max.apply(null, this.option.series[0].data);
    // 蒸发量
    this.option.series[0].data=tpldata[0].zhengFaLiang.split(",");
    //降水量
    this.option.series[1].data=tpldata[0].jiangShuiLiang.split(",");
    // 平均温度
    this.option.series[2].data=tpldata[0].pingJunWenDu.split(",");
    
    // 使用刚指定的配置项和数据显示图表。
    myChart.setOption(this.option);
  }
};
</script>

<style>
</style>
