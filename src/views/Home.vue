<template>
  <div class="home">
    <h1>呼叫工作台自定义弹屏参数测试页面</h1>
    <!-- 表格展示options  左右间距20%  居中展示表格 -->
    <el-table :data="options" style="width: 40%; margin: 0 auto;">
      <el-table-column prop="name" label="name"></el-table-column>
      <el-table-column prop="key" label="key"></el-table-column>
      <el-table-column prop="value" label="value"></el-table-column>
    </el-table>
  </div>
</template>

<script lang="ts">
import { reactive } from 'vue';
import { Vue } from 'vue-class-component';
export default class Home extends Vue {
  options: any = reactive([]);
  kv: any = reactive([
    {
      key: 'enterpriseId',
      name: '企业ID'
    },
    {
      key: 'hotline',
      name: '热线号码'
    },
    {
      key: 'cno',
      name: '员工号码'
    },
    {
      key: 'callType',
      name: '呼叫类型'
    },
    {
      key: 'customerNumber',
      name: '客户号码'
    },
    {
      key: 'uniqueId',
      name: '呼叫唯一标识'
    },
    {
      key: 'customerNumberType',
      name: '客户号码类型'
    },
    {
      key: 'customerNumberAreaCode',
      name: '客户号码区号'
    },
    {
      key: 'numberTrunk',
      name: '中继号码'
    },
    {
      key: 'qno',
      name: '队列号码'
    },
    {
      key: 'qname',
      name: '队列名称'
    },
    {
      key: 'mainUniqueId',
      name: '主叫呼叫唯一标识'
    },
    {
      key: 'consulterCno',
      name: '咨询来源坐席号'
    },
    {
      key: 'transferCno',
      name: '转移来源坐席号'
    },
    {
      key: 'crmId',
      name: 'CRM客户ID'
    },
    {
      key: 'ivrId',
      name: 'IVR流程ID'
    },
    {
      key: 'ivrName',
      name: 'IVR流程名称'
    }
  ]);

  created() {
    const obj = this.$route.query
    // 将obj 与 kv 进行匹配 生成 options ,按照kv 的顺序进行排序,未匹配的放在最后
    this.kv.forEach((item: any) => {
      if (obj[item.key]) {
        this.options.push({
          name: item.name,
          key: item.key,
          value: obj[item.key]
        });
      }
    });
    Object.keys(obj).forEach((key: any) => {
      if (!this.options.find((item: any) => item.key === key)) {
        this.options.push({
          name: '自定义参数',
          key,
          value: obj[key]
        });
      }
    });
  }
}
</script>
