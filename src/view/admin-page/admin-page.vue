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
  name: 'user-page',
  components: {
    Tables
  },
  data () {
    return {
      columns: [
        {title: '工号', key: 'id', sortable: true, width: 120},
        {title: '姓名', key: 'name', sortable: true, width: 110},
        {title: '性别', key: 'sex', editable: false, width: 100},
        {title: '手机号', key: 'phone', width: 130},
        {title: '出生年月', key: 'birthday', width: 110},
        {title: '部门', key: 'department', width: 120},
        {
          title: '删除',
          key: 'handle',
          options: ['delete'],
          button: [
            (h, params, vm) => {
              return h('Poptip', {
                props: {
                  confirm: true,
                  title: '你确定要删除吗?'
                },
                on: {
                  'on-ok': () => {
                    vm.$emit('on-delete', params)
                    vm.$emit('input', params.tableData.filter((item, index) => index !== params.row.initRowIndex))
                  }
                }
              })
            }
          ],
        }
      ],
      tableData: [],

    }
  },
  methods: {
    handleDelete (params) {
      console.log('delete');
    },
    handleClick (params) {
    
    },
    fetchData () {
      
    }

  },
  mounted () {
    getTableData().then(res => {
      res.data = [
        {
          'id': '10001',
          'name': '张三',
          'sex': '男',
          'phone': '18888888888',
          'birthday': '1998-09-23',
          'department': '技术部'
        },
        {
          'id': '10002',
          'name': '王美丽',
          'sex': '女',
          'phone': '18888888888',
          'birthday': '1998-09-23',
          'department': '财务部'
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
    .ivu-poptip-body{
      text-align: left; 
    }
  }
</style>

