<template>
  <div class="percent" ref="percent"></div>
</template>

<script>
export default {
  mounted() {
    this.drawPie();//绘制图标函数
  },
  data() {
    return {
      // 图表配置项
      pieData:[
                  //第一个圆环图
                    {
                      name: "左",   
                      data: [
                        {
                          name: "",
                          value: "37"
                        },
                        {
                          name: "3",
                          value: "5"
                        },
                        {
                          name: "1",
                          value: "24"
                        },
                        {
                          name: "2",
                          value: "15"
                        },
                        {
                          name: "6",
                          value: "2"
                        },
                        {
                          name: "5",
                          value: "3"
                        }
                      ]
                    },
                //第二个圆环图
                    {
                      name: "中",
                      data: [
                        {
                          name: "",
                          value: "37"
                        },
                        {
                          name: "3",
                          value: "5"
                        },
                        {
                          name: "1",
                          value: "24"
                        },
                        {
                          name: "2",
                          value: "15"
                        },
                        {
                          name: "6",
                          value: "2"
                        },
                        {
                          name: "5",
                          value: "3"
                        }
                      ]
                    }, 
                    //第三个圆环图
                    {
                      name: "右",
                      data: [
                        {
                          name: "",
                          value: "37"
                        },
                        {
                          name: "3",
                          value: "5"
                        },
                        {
                          name: "1",
                          value: "24"
                        },
                        {
                          name: "2",
                          value: "15"
                        },
                        {
                          name: "6",
                          value: "2"
                        },
                        {
                          name: "5",
                          value: "3"
                        }
                      ]
                    }
                  ],
      option:{
                  color:['#4472C5','#ED7C30','#80FF80','#FF8096','#800080'],//配置颜色
                  tooltip: {
                    trigger: "item",
                    formatter: "{a} <br/>{b} : {c} ({d}%)"
                  },
                  // 图例
                  legend: {
                    type: "scroll",
                    // orient: "vertical",
                    top: 20,
                    left: "center",
                    data: [], //图例数据从后台获取
                    textStyle: {
                      //图例文字的样式
                      color: "#999",//['#4472C5','#ED7C30','#80FF80','#FF8096','#800080']不同样式
                      fontSize: 12
                    }
                  },
                  // 直角坐标系内绘图网格
                  grid: {
                    left: "3%",
                    right: "4%",
                    bottom: "30%",
                    containLabel: true
                  },
                  //图表展示数据从后台获取
                  series: []
                },
    };
  },

  methods: {
     getChartData() {
      // 图例legend数据
      let legendData = [];
      //this.pieData为后台返回数据
      if (this.pieData) {
        for (let i = 0; i < this.pieData[0].data.length; i++) {
          legendData.push(this.pieData[0].data[i].name);
        }
        this.option.legend.data = legendData;
        // this.option.series[0].name = legendData;
        var center;
        for (var i in this.pieData) {
          center = 100 / (2 + Number(i));
        }
 
        for (var i = 0; i < this.pieData.length; i++) {
          this.option.series[i] = {
            name: this.pieData[i].name,
            type: "pie",       
            center: [center * Number(i + 1) + "%", "60%"],     //每个圆环图的位置，动态计算
            //第一个是内径。第二个是外径。内劲变大就是圆环
            radius: [center + "%", center + center + "%"],     //每个圆环图的大小，动态计算
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: false,
                position: "center"
              },
              emphasis: {
                show: true,
                textStyle: {
                  fontSize: "30",
                  fontWeight: "bold"
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: []
          };
          this.option.series[i].data = this.pieData[i].data;
        }
      } else {
        this.option.legend.data = [];
        this.option.series[0].data = [];
      }
    },
    drawPie() {
      // 获取数据
      this.getChartData();
      let percent = this.$refs.percent;
      // 核心代码：
      // 基于准备好的dom，初始化echarts实例
      let pieChart = this.$echarts.init(percent);
      // 绘制图表
      pieChart.setOption(this.option);
    },
  }
};
</script>

<style lang='stylus'>
.percent {
  width: 90%;
  height: 13rem;
  margin: 0 auto;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0rem 0rem 1rem #adadad;
}
</style>