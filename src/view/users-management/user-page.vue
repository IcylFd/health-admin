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
      <!-- <Button style="margin: 10px 0;" type="primary" @click="exportExcel">导出为Csv文件</Button> -->
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
        {title: 'ID', key: 'id', sortable: true, width: 70},
        {title: '姓名', key: 'name', sortable: true, width: 80},
        {title: '性别', key: 'sex', editable: false, width: 60},
        {title: '手机号', key: 'phone', width: 110},
        {title: '出生年月', key: 'birthday', width: 100},
        {title: '身高(cm)', key: 'height', sortable: true, width: 103},
        {title: '体重(kg)', key: 'weight', sortable: true, width: 100},
        {title: '血型', key: 'blood', width: 60},
        {title: '默认紧急联系人姓名', key: 'contact_name',width:120},
        {title: '默认紧急联系人电话', key: 'contact_num',width:120},
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
          'birthday': '1998-09-23',
          'height': '180',
          'weight': '60',
          'blood': 'A',
          'contact_name': '李大明',
          'contact_num': '17777777777',
          'warning': true,
          'warning_msg': 'aaaaaaa'
        },
        {
          'id': '2',
          'name': '王小兰',
          'sex': '女',
          'phone': '18888888888',
          'birthday': '1998-09-23',
          'height': '180',
          'weight': '60',
          'blood': 'A',
          'contact_name': '王小红',
          'contact_num': '17777777777',
          'warning': false,
          'warning_msg': ''
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

