<template>
  <div>
    <el-table :data="tableData">
      <el-table-column
          v-for="column in columns"
          :key="column.prop"
          :prop="column.prop"
          :label="column.label"
      >
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "testName",
  data() {
    return {
      columns: [
        { label: '姓名', prop: 'name' },
        { label: '年龄', prop: 'age' },
      ],
      tableData: [
        { name: '张三', age: 18 },
        { name: '李四', age: 20 },
      ],
    };
  },
  methods: {
    // 动态添加列
    addColumn() {
      this.columns.push({ label: '性别', prop: 'gender' });
      this.tableData.forEach((item) => {
        this.$set(item, 'gender', '男');
      });
    },
  },
};
</script>
