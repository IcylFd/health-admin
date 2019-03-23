<template lang="html">
  <div id="example">
    <ul class="switch-list">
      <li class="switch-item" v-for="item in propList">
        <span>{{ item.name }}: </span>
        <zk-switch v-model="props[item.name]"></zk-switch>
      </li>
    </ul>
    <tree-table
      ref="table"
      sum-text="sum"
      index-text="#"
      :data="data"
      :columns="columns"
      :stripe="props.stripe"
      :border="props.border"
      :show-header="props.showHeader"
      :show-summary="props.showSummary"
      :show-row-hover="props.showRowHover"
      :show-index="props.showIndex"
      :tree-type="props.treeType"
      select-type="radio"
      :is-fold="props.isFold"
      :expand-type="props.expandType"
      expand-key="sex"
      @radio-click="handleRadioClick"
      :selection-type="props.selectable">
      <!-- <tree-table
        :columns="columns"
        :expand-type="false"
        :selection-type="false"
        :data="data"> -->
      <template slot="$expand" slot-scope="scope">
        {{ `My name is ${scope.row.name},
           this rowIndex is ${scope.rowIndex}.`
         }}
      </template>
      <template slot="likes" slot-scope="scope">
        <button>123</button>
      </template>
    </tree-table>
  </div>
</template>

<script>
  import ZkSwitch from './Switch/Switch';

  export default {
    name: 'example',
    components: {
      ZkSwitch,
    },
    data() {
      return {
        props: {
          stripe: false,
          border: false,
          showHeader: true,
          showSummary: false,
          showRowHover: true,
          showIndex: false,
          treeType: true,
          isFold: true,
          expandType: false,
          selectable: false,
        },
        data: [
          {
            name: 'Jack',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 10,
            children: [
              {
                name: 'Ashley',
                sex: 'female',
                likes: ['football', 'basketball'],
                score: 20,
                children: [
                  {
                    name: 'Ashley',
                    sex: 'female',
                    likes: ['football', 'basketball'],
                    score: 20,
                  },
                  {
                    name: 'Taki',
                    sex: 'male',
                    likes: ['football', 'basketball'],
                    score: 10,
                    children: [
                      {
                        name: 'Ashley',
                        sex: 'female',
                        likes: ['football', 'basketball'],
                        score: 20,
                      },
                      {
                        name: 'Taki',
                        sex: 'male',
                        likes: ['football', 'basketball'],
                        score: 10,
                        children: [
                          {
                            name: 'Ashley',
                            sex: 'female',
                            likes: ['football', 'basketball'],
                            score: 20,
                          },
                          {
                            name: 'Taki',
                            sex: 'male',
                            likes: ['football', 'basketball'],
                            score: 10,
                          },
                        ],
                      },
                    ],
                  },
                ],
              },
              {
                name: 'Taki',
                sex: 'male',
                likes: ['football', 'basketball'],
                score: 10,
              },
            ],
          },
          {
            name: 'Tom',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 20,
            children: [
              {
                name: 'Ashley',
                sex: 'female',
                likes: ['football', 'basketball'],
                score: 20,
                children: [
                  {
                    name: 'Ashley',
                    sex: 'female',
                    likes: ['football', 'basketball'],
                    score: 20,
                  },
                  {
                    name: 'Taki',
                    sex: 'male',
                    likes: ['football', 'basketball'],
                    score: 10,
                  },
                ],
              },
              {
                name: 'Taki',
                sex: 'male',
                likes: ['football', 'basketball'],
                score: 10,
                children: [
                  {
                    name: 'Ashley',
                    sex: 'female',
                    likes: ['football', 'basketball'],
                    score: 20,
                  },
                  {
                    name: 'Taki',
                    sex: 'male',
                    likes: ['football', 'basketball'],
                    score: 10,
                  },
                ],
              },
            ],
          },
          {
            name: 'Tom',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 20,
          },
          {
            name: 'Tom',
            sex: 'male',
            likes: ['football', 'basketball'],
            score: 20,
            children: [
              {
                name: 'Ashley',
                sex: 'female',
                likes: ['football', 'basketball'],
                score: 20,
              },
              {
                name: 'Taki',
                sex: 'male',
                likes: ['football', 'basketball'],
                score: 10,
              },
            ],
          },
        ],
        columns: [
          {
            title: 'name',
            key: 'name',
            width: '400px',
          },
          {
            title: 'sex',
            key: 'sex',
            minWidth: '50px',
          },
          {
            title: 'score',
            key: 'score',
          },
          {
            title: 'likes',
            key: 'likes',
            minWidth: '200px',
            type: 'template',
            template: 'likes',
          },
        ],
      };
    },
    computed: {
      propList() {
        return Object.keys(this.props).map(item => ({
          name: item,
        }));
      },
    },
    methods: {
      handleRadioClick(option) {
        console.log(option); // eslint-disable-line
      },
    },
  };
</script>

<style scoped lang="less">
  * {
    margin: 0;
    padding: 0;
  }

  .switch-list {
    margin: 20px 0;
    list-style: none;
    overflow: hidden;
  }

  .switch-item {
    margin: 20px;
    float: left;
  }
</style>
