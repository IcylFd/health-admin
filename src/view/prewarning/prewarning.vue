<template>
  <div>
    <Card>
      <tables ref="tables" 
              editable 
              searchable 
              search-place="top" 
              v-model="tableData" 
              :columns="columns" 
              @on-delete="handleDelete" 
              class="user-table"
              @on-row-click="handleClick"
      />
    </Card>
  </div>
</template>

<script>
import axios from 'axios'
import Tables from '_c/tables'
import { getTableData } from '@/api/data'
export default {
  name: 'prewarning',
  components: {
    Tables
  },
  data () {
    return {
      columns: [
        {title: 'ID', key: 'id', sortable: true, width: 70},
        {title: '姓名', key: 'name', sortable: true, width: 80},
        {title: '性别', key: 'sex', editable: false, width: 60},
        {title: '手机号', key: 'phone', width: 120},
        {title: '预警位置', key: 'warning_pos', width: 170},
        {title: '预警信息', key: 'warning_msg', width: 170},
        {title: '预警时间', key: 'warning_time', width: 140},
        {title: '默认紧急联系人姓名', key: 'contact_name'},
        {title: '默认紧急联系人电话', key: 'contact_num'},
      ],
      tableData: [],

    }
  },
  methods: {
    handleDelete (params) {
    },
    handleClick (params) {
      this.$router.push({
        name: 'user_health',
        params: params,
      });
    },
    getUserData () {
      axios.get("https://api.myjson.com/bins/rr166").then(res => {
        for(var i = 0; i < res.data.length; i++){
          if(res.data[i].warning){
            this.tableData.push(res.data[i]);
          }
        }
          
      });
    }

  },
  mounted () {
    this.getUserData();
  }
}
</script>

<style lang="less">
  .user-table{
    .ivu-table th,
    .ivu-table-cell{
      text-align: center;
    }
    .ivu-btn-ghost{
      z-index: 999;
      outline-style: none;
    }
    .ivu-poptip-body{
      text-align: left; 
    }
  }
</style>

