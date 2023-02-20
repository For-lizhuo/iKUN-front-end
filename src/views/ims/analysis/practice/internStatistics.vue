<template>
  <div id='app'>
    <el-row class="dashboard-editor-container">
      <el-card shadow="hover" class="border-radius8">
        <iKUN-plate-group :info-list="infoCardData"/>
      </el-card>
    </el-row>
    <el-row class="dashboard-editor-container" :gutter="32">
      <el-col :xs="24" :sm="34" :lg="24">
        <el-card class="text-center border-radius8">
          <iKUN-bar-chart :width="width" ref="barData" />
        </el-card>
      </el-col>
      <!-- <el-col :xs="24" :sm="24" :lg="10">
        <el-card class="text-center border-radius8">
          <iKUN-pie-chart :width="width" ref="pieData" />
        </el-card>
      </el-col> -->
    </el-row>
    <el-row class="dashboard-editor-container">
      <el-card class="border-radius8">
        <el-table v-loading="loading" :data="tableData" border :header-cell-style="{background:'#DCDFE6'}"  >
          <el-table-column label="院系" align="center" prop="deptName" />
          <el-table-column label="实习结束人数" align="center" prop="columnNum1" />
          <el-table-column label="实习中人数" align="center" prop="columnNum2" />
          <el-table-column label="未实习人数" align="center" prop="columnNum3" />
        </el-table>
      </el-card>
    </el-row>
  </div>
</template>

<script>
import iKUNBarChart from "../components/chart/barChart";
import iKUNPieChart from "../components/chart/pieChart";
import iKUNPlateGroup from "../components/plateGroup";
export default {
  name: "internStatistics",
  components: {
    iKUNPlateGroup,
    iKUNPieChart,
    iKUNBarChart
  },
  props:{
    className:{
      type:String,
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '360px'
    }
  },
  data(){
    return {
      loading: false,
      //plate数据
      plateData: {},
      //柱形图数据
      barData: {},
      //饼形图数据
      pieData: {},
      //plate数据
      infoCardData: [],
      // 数据列表
      tableData:[{
        deptName:'软件学院',
        columnNum1:10,
        columnNum2:2,
        columnNum3:20
      },{
        deptName:'计算机科学与技术学院',
        columnNum1:23,
        columnNum2:6,
        columnNum3:16
      },{
        deptName:'电子信息与通信技术学院',
        columnNum1:16,
        columnNum2:5,
        columnNum3:17
      },{
        deptName:'网络空间与安全学院',
        columnNum1:7,
        columnNum2:1,
        columnNum3:10
      }]
    }
  },
  methods: {
    getAnalysisValue(m){
      // this.infoCardData = m.internshipPlate;
      this.infoCardData = [{count:56,title:"实习结束人数"},{count:14,title:"实习中人数"},{count:63,title:"未实习人数"},]
      this.tableData = [{
        deptName:'软件学院',
        columnNum1:10,
        columnNum2:2,
        columnNum3:20
      },{
        deptName:'计算机科学与技术学院',
        columnNum1:23,
        columnNum2:6,
        columnNum3:16
      },{
        deptName:'电子信息与通信技术学院',
        columnNum1:16,
        columnNum2:5,
        columnNum3:17
      },{
        deptName:'网络空间与安全学院',
        columnNum1:7,
        columnNum2:1,
        columnNum3:10
      }];
      const legendData = ['实习结束人数', '实习中人数', '未实习人数'];
      let obj = {
        xAxisData: ['软件学院','计算机学院','电子信息与通信技术学院','网络工程与安全学院'],
        seriesData2: [2,6,5,1],
        seriesData1: [10,23,16,7],
        seriesData3: [20,26,17,10],
        legendData: legendData,
        seriesName1: '实习结束人数',
        seriesName2: '实习中人数',
        seriesName3: '未实习人数',
      }
      this.barData = obj;
      this.$refs.barData.getBarData(this.barData);
      //重构m.internshipPlate数据，变成pieData
      //const seriesData = this.refactorListToPieData(m.internshipPlate);
      //const legendData = ['实习结束人数', '实习中人数', '未实习人数'];
      const name = '实习人数统计';
      let pieObj = {
        seriesData: seriesData,
        legendData: legendData,
        seriesName: name
      }
      this.$refs.pieData.getPieData(pieObj);
    },
    /** 重构 m.internshipPlate数据，变成pieData  */
    refactorListToPieData(list){
      let j = 0, len = list.length;
      const array = [];
      for(; j < len; j++) {
        var object = {
          value: null,
          name: null,
        };
        for(var key in list[j]){
          if (key === 'count'){
            object.value = list[j][key]
          }else {
            object.name = list[j][key]
          }
        }
        array.push(object);
      }
      return array;
    }
  },
}
</script>

<style scoped>
  .dashboard-editor-container {
    padding: 10px;
    background-color: #F2F6FC;
    position: relative;
  }
</style>
