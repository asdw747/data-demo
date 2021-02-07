<template>
  <div class="dashboard-container">
    <div class="Echarts" style="width: 1100px; height: 400px; margin-left: 80px; margin-bottom: 100px;">
      <div style="float: left;width: 300px;height:300px;margin-right: 50px">
        数据输入
        <textarea rows="15" cols="15" style="width: 300px; margin-top: 10px" v-model="input1"/>
      </div>
      <div style="float: left;height: 300px;margin-right: 10px">
        <button type="submit" style="margin-top: 150px" @click="convert">转换</button>
      </div>
      <div id="main" style="float: left;width: 600px;height:400px;"/>
    </div>

    <div style="border: 0.5px solid rgb(209, 204, 204);width:1360px;height:0;margin-top: -80px;margin-bottom: 40px"></div>

    <div class="Echarts" style="width: 1000px; height: 500px; margin-left: 80px;">
      <div id="main2" style="float: left;width: 800px;height:400px;"></div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  data() {
    return {
      input1: "",
      input2: null,
    }
  },
  methods: {
    convert() {
      console.log(this.input1)
      var json
      try {
        json = JSON.parse(this.input1)
        console.log(json)
      } catch (e) {
        alert("非法json格式")
        return;
      }

      if (json == null || json == "") {
        return;
      }

      var key = [];
      var value = [];
      for(var item in json){//遍历json对象的每个key/value对
        console.log(item + json[item])
        key.push(item)
        value.push(json[item])
      }

      var myChart = this.$echarts.init(document.getElementById('main'));

      // 指定图表的配置项和数据
      var option = {
        title: {
          text: '演示表格'
        },
        tooltip: {},
        legend: {
          data:['销量']
        },
        xAxis: {
          data: key
        },
        yAxis: {},
        series: [{
          name: 'output',
          type: 'bar',
          data: value
        }]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    },

    myEcharts() {
      // 基于准备好的dom，初始化echarts实例
      var myChart = this.$echarts.init(document.getElementById('main'));

      // 指定图表的配置项和数据
      var option = {
        title: {
          text: '演示表格'
        },
        tooltip: {},
        legend: {
          data:['销量']
        },
        xAxis: {
          data: ["A","B","C","D","E","F"]
        },
        yAxis: {},
        series: [{
          name: 'output',
          type: 'bar',
          data: [5, 20, 36, 10, 10, 20]
        }]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    },

    myEcharts2(){
      // 基于准备好的dom，初始化echarts实例
      var myChart2 = this.$echarts.init(document.getElementById('main2'));

      // 指定图表的配置项和数据
      var option = {
        title: {
          text: '折线图堆叠'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['A', 'B', 'C', 'D', 'E']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['A', 'B', 'C', 'D', 'F', 'G', 'H']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '邮件营销',
            type: 'line',
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: '视频广告',
            type: 'line',
            stack: '总量',
            data: [150, 232, 201, 154, 190, 330, 410]
          },
          {
            name: '直接访问',
            type: 'line',
            stack: '总量',
            data: [320, 332, 301, 334, 390, 330, 320]
          },
          {
            name: '搜索引擎',
            type: 'line',
            stack: '总量',
            data: [820, 932, 901, 934, 1290, 1330, 1320]
          }
        ]
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart2.setOption(option);
    }
  },

  mounted() {
    this.myEcharts()
    this.myEcharts2()
  },
  computed: {
    ...mapGetters([
      'name'
    ])
  },
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
