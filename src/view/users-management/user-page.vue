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
import axios from 'axios'
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
    },
    getUserData () {
      axios.get("https://api.myjson.com/bins/rr166").then(res => {
          this.tableData = res.data;
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

