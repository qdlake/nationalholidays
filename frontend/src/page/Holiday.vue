<template>
  <div class="list ">
    <el-table :data="holidays" highlight-current-row v-loading="loading" @selection-change="selsChange" style="width: 100%;">
      <el-table-column type="selection" width="55">
      </el-table-column>
      <el-table-column type="index" width="60">
      </el-table-column>
      <el-table-column prop="day" label="假日日期" width="120" sortable>
      </el-table-column>
      <el-table-column prop="name" label="假日名称" width="150" sortable>
      </el-table-column>
      <el-table-column prop="prop" label="假日类别" width="150" sortable>
      </el-table-column>
      <el-table-column prop="desc" label="假日说明" min-width="200" sortable>
      </el-table-column>
      <el-table-column label="操作" width="150">
        <template scope="scope">
          <el-button size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button type="danger" size="small" @click="handleDel(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
  import { getHolidays } from '../api/api';
  export default {
    data() {
      return {
        loading: false,
        holidays: [],
        sels: []
      }
    },
    watch: {
      '$route': 'getHolidays'
    },
    methods: {
      getHolidays: function () {
        this.loading = true;
        let param = {
          nation: this.$route.params.nation,
          year: this.$route.params.year
        };
        getHolidays(param).then((res) => {
          this.holidays = res.data.data;
          this.loading = false;
        });
      },
      selsChange: function (sels) {
        this.sels = sels;
      }
    },
    mounted () {
      this.getHolidays();
    }
  };

</script>
