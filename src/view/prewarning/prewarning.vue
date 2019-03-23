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
        {title: '姓名', key: 'name', sortable: true, width: 100},
        {title: '性别', key: 'sex', editable: false, width: 70},
        {title: '手机号', key: 'phone', width: 180},
        {title: '预警信息', key: 'warning_msg'},
        {title: '默认紧急联系人姓名', key: 'contact_name',width:180},
        {title: '默认紧急联系人电话', key: 'contact_num',width:180},
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
    }

  },
  mounted () {
    getTableData().then(res => {
      res.data = [
        {
          'id': '1',
          'name': '王小明',
          'sex': '男',
          'phone': '18888888888',
          'warning_msg':'aaaaaaaaaaaaaaaa',
          'contact_name': '李大明',
          'contact_num': '17777777777'
        },
        {
          'id': '2',
          'name': '王小兰',
          'sex': '女',
          'phone': '18888888888',
          'warning_msg':'aaaaaaaaaaaaaaaa',
          'contact_name': '王小红',
          'contact_num': '17777777777'
        }
      ];
      this.tableData = res.data;
      
    })
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

