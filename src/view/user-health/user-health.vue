<template>
  <div class="user-health">
    <div class="user-card">
      <div class="user-main">
        <div class="user-img">
          <img src="" alt="">
        </div>
        <div class="user-main-info">
          <p>No.{{user_msg.id}}</p>
          <p>{{user_msg.name}}</p>
          <p>电话：{{user_msg.phone}}</p>
        </div>
      </div>
      <div class="user-info">
        <div v-if="user_msg.warning">
          <p><Icon type="ios-navigate-outline" size="20" color="#c23531"/>预警位置信息：{{user_msg.warning_pos}}</p>
          <p><Icon type="ios-clock-outline" size="20" color="#c23531"/>预警时间：{{user_msg.warning_time}}</p>
          <p><Icon type="ios-create-outline" size="20" color="#c23531"/>预警信息内容：{{user_msg.warning_msg}}</p>
        </div>
        <div v-else>
          <p style="color: #2d8cf0">该用户暂无预警信息</p>
        </div>
        <p><Icon type="ios-contacts-outline" size="20"/>紧急联系人姓名：{{user_msg.contact_name}}</p>
        <p><Icon type="ios-call-outline" size="20"/>紧急联系人电话：{{user_msg.contact_num}}</p>
      </div>
    </div>
    <Row class="chart">
      <div class="chart-title">近一周每日指标均值</div>
      <Card shadow>
        <example style="height: 310px;"/>
      </Card>
    </Row>
  </div>
</template>

<script>
import Example from './example.vue'
export default {
  name: 'user-health',
  components: {
      Example
  },
  data () {
    return {
      user_msg: this.$route.params,
    }
  },
  methods: {
    
  },


}
</script>

<style lang="less" scoped>
  .user-health {
    .user-card {
      width: 80%;
      height: 300px;
      background: #fff;
      border-radius: 20px;
      font-size: 14px;
      display: flex;
      margin: 0 auto;
    }
    .user-main {
      flex: 1;
      width: 20%;
      height: 300px;
      margin: 0 30px;
      padding: 20px 0;
      text-align: center;
    }
    .user-img{
      width: 100px;
      height: 100px;
      margin: 0 auto;
      background: url('../../assets/images/user.png') no-repeat center;
      background-size: cover;
    }
    .user-main-info{
      margin-top: 10px;
    }
    .user-info{
      flex: 3;
      width: 80%;
      padding: 40px 0;
      p{
        line-height: 32px;
        // float: left;
        // display: inline;
      }
      .ivu-icon{
        margin-right: 5px;
      }
    }
    .chart{
      margin-top: 30px;
      .chart-title{
          font-size: 14px;
          margin-bottom: 10px;
      }
    }
  }
</style>

