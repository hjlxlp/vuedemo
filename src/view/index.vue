<template>
  <el-table :data="tableData" border stripe style="width: 100% ">

    <el-table-column prop="classname" label="价值观" width="180" align="center">
    </el-table-column>
    <el-table-column prop="kpiname" label="Our Behaviors" width="180" align="center">
    </el-table-column>
    <el-table-column prop="leading" label="领导自己" width="180" align="center">
    </el-table-column>

    <el-table-column prop="date" label="目标" width="180" align="center">
      <el-table-column :label="item" v-for="(item, index) in header" :key="index" align="center">
        <template slot-scope="scope">
          <el-input v-model="scope.row.kpilist[index].content" @change="rowItemChange(scope.row.kpilist[index])"></el-input>
        </template>
      </el-table-column>
    </el-table-column>

      <el-table-column prop="resultname" label="结果" width="180" align="center">
        <template slot-scope="scope">
          <el-input v-model="scope.row.resultname" @change="rowChange(scope.row)"></el-input>
        </template>
      </el-table-column>
    <el-table-column prop="result" label="是/否" width="180" align="center">
      <template slot-scope="scope">
        <el-input v-model="scope.row.result" @change="rowChange(scope.row)"></el-input>
      </template>
    </el-table-column>
    <el-table-column prop="remark" label="备注" width="180" align="center">
      <template slot-scope="scope">
        <el-input v-model="scope.row.remark" @change="rowChange(scope.row)"></el-input>
      </template>
    </el-table-column>

  </el-table>
</template>

<script>
export default {
  name: "indexName",
  data() {
    return {
      header : ["CG3","CG4","CG5"],
      tableData: [
        {
          "kpilist": [
            {
              "kpiid": 6,
              "autoid": 17,
              "content": "8",
              "hrlevel": "CG3"
            },
            {
              "kpiid": 6,
              "autoid": 18,
              "content": "10",
              "hrlevel": "CG4"
            },
            {
              "kpiid": 6,
              "autoid": 19,
              "content": "12",
              "hrlevel": "CG5"
            }
          ],
          "classname": "彼此信任",
          "orderindex": 3,
          "instanceid": "ffceae93-4a54-42b3-a0b1-58027f022c2b",
          "kpiid": 6,
          "kpiname": "质量",
          "resultname": "1",
          "result": "2",
          "remark": "3",
          "leading": "质量导向"
        },
        {
          "kpilist": [
            {
              "kpiid": 7,
              "autoid": 20,
              "content": "8",
              "hrlevel": "CG3"
            },
            {
              "kpiid": 7,
              "autoid": 21,
              "content": "10",
              "hrlevel": "CG4"
            },
            {
              "kpiid": 7,
              "autoid": 22,
              "content": "12",
              "hrlevel": "CG5"
            }
          ],
          "classname": "全力拼搏",
          "orderindex": 3,
          "instanceid": "ffceae93-4a54-42b3-a0b1-58027f022c2b",
          "kpiid": 7,
          "kpiname": "结果导向",
          "resultname": "",
          "result": "",
          "remark": "",
          "leading": "规划与组织"
        },
        {
          "kpilist": [
            {
              "kpiid": 8,
              "autoid": 23,
              "content": "8",
              "hrlevel": "CG3"
            },
            {
              "kpiid": 8,
              "autoid": 24,
              "content": "10",
              "hrlevel": "CG4"
            },
            {
              "kpiid": 8,
              "autoid": 25,
              "content": "12",
              "hrlevel": "CG5"
            }
          ],
          "classname": "自主而为",
          "orderindex": 3,
          "instanceid": "ffceae93-4a54-42b3-a0b1-58027f022c2b",
          "kpiid": 8,
          "kpiname": "主人翁意识",
          "resultname": "",
          "result": "",
          "remark": "",
          "leading": "展现主人翁意识"
        },
        {
          "kpilist": [
            {
              "kpiid": 9,
              "autoid": 26,
              "content": "8",
              "hrlevel": "CG3"
            },
            {
              "kpiid": 9,
              "autoid": 27,
              "content": "10",
              "hrlevel": "CG4"
            },
            {
              "kpiid": 9,
              "autoid": 28,
              "content": "12",
              "hrlevel": "CG5"
            }
          ],
          "classname": "同舟共济",
          "orderindex": 3,
          "instanceid": "ffceae93-4a54-42b3-a0b1-58027f022c2b",
          "kpiid": 9,
          "kpiname": "协作",
          "resultname": "",
          "result": "",
          "remark": "",
          "leading": "协作"
        }
      ]
    }
  },
  methods: {
    // 修改行内字段
    rowChange(row) {
      // todo 调用后端接口，根据kpiid，修改resultname，result，remark
      // row代表一行
      //alert(row);
      console.log("kpiid：" + row.kpiid)
      console.log("resultname：" + row.resultname)
      console.log("result：" + row.result)
      console.log("remark：" + row.remark)

      // 重新统计，这里要先移除最后一行
      this.tableData.pop()
      this.recalculateKpi()
    },
    // 修改行内list的某个字段
    rowItemChange(rowItem) {
      // todo 调用后端接口，根据autoid，修改content
      // rowItem代表一行里面的某个目标
      //alert(rowItem);
      console.log("autoid：" + rowItem.autoid)
      console.log("content：" + rowItem.content)

      // 重新统计，这里要先移除最后一行
      this.tableData.pop()
      this.recalculateKpi()
    },
    // 重新统计
    recalculateKpi() {
      // 最后一行
      let last = {}
      // 最后一行的kpilist
      let lastkpilist = []
      for (let i = 0; i < this.header.length; i++) {
        // 找出这列的所有kpi并计算求和
        const sum = this.tableData.reduce((acc, cur) => {
          return acc + Number(cur.kpilist[i].content)
        }, 0)
        let kpi = {}
        kpi.content = sum
        lastkpilist.push(kpi)
      }
      last.kpilist = lastkpilist
      // 计算结果列的统计
      last.resultname = this.tableData.reduce((acc, cur) => {
        return acc + Number(cur.resultname)
      }, 0)
      // 添加到list
      this.tableData.push(last)
    },
  },
  created() {
    //todo 查询数据库接口数据
    //this.header = []
    //this.tableData = []

    // 统计数据
    this.recalculateKpi()

  }
}
</script>

<style scoped>

</style>