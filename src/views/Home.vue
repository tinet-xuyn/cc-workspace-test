<template>
  <div class="home">
    <h1>呼叫工作台自定义弹屏参数测试页面</h1>
    <!-- 表格展示options  左右间距20%  居中展示表格 -->
    <el-table :data="options" style="width: 40%; margin: 0 auto">
      <el-table-column prop="name" label="name"></el-table-column>
      <el-table-column prop="key" label="key"></el-table-column>
      <el-table-column prop="value" label="value"></el-table-column>
    </el-table>
  </div>
</template>

<script lang="ts">
import { reactive, watch } from "vue";
import { Vue } from "vue-class-component";
export default class Home extends Vue {
  options: any = reactive([]);
  kv: any = [
    {
      key: "enterpriseId",
      name: "企业ID",
      id: 1,
    },
    {
      key: "hotline",
      name: "热线号码",
    },
    {
      key: "cno",
      name: "员工号码",
    },
    {
      key: "callType",
      name: "呼叫类型",
    },
    {
      key: "customerNumber",
      name: "客户号码",
    },
    {
      key: "uniqueId",
      name: "呼叫唯一标识",
    },
    {
      key: "customerNumberType",
      name: "客户号码类型",
    },
    {
      key: "customerNumberAreaCode",
      name: "客户号码区号",
    },
    {
      key: "numberTrunk",
      name: "中继号码",
    },
    {
      key: "qno",
      name: "队列号码",
    },
    {
      key: "qname",
      name: "队列名称",
    },
    {
      key: "mainUniqueId",
      name: "主叫呼叫唯一标识",
    },
    {
      key: "consulterCno",
      name: "咨询来源坐席号",
    },
    {
      key: "transferCno",
      name: "转移来源坐席号",
    },
    {
      key: "crmId",
      name: "CRM客户ID",
    },
    {
      key: "ivrId",
      name: "IVR流程ID",
    },
    {
      key: "ivrName",
      name: "IVR流程名称",
    },
  ];
  
  mounted() {
    this.$watch('$route', this.onRouteChanged);
    this.init();
  }

  onRouteChanged(newRoute: any, oldRoute: any) {
    // 在这里处理路由变化的逻辑
    console.log('Route changed:', newRoute, oldRoute);
    this.init();
    // 处理逻辑...
  }

  init() {
    this.options = [];
    const obj = this.$route.query;
    // 将对象转换为数组 并且匹配 kv 并且按照kv的顺序展示 如果未匹配则name为自定义 并且放在最后展示
    for (const key in obj) {
      // 判断 key 是否在 kv 中
      this.options.push({
        key,
        value: obj[key],
        name: this.kv.find((c: any) => c["key"] === key)?.name || "自定义",
      });
    }
    this.options = this.options.sort(this.compareFn);
  }

  compareFn(a: any, b: any) {
    let index1 = this.kv.findIndex((v: any) => v.name === a.name);
    let index2 = this.kv.findIndex((v: any) => v.name === b.name);
    if (index1 === -1) {
      return 1; // 将不存在的元素放到最后
    }

    if (index2 === -1) {
      return -1; // 将不存在的元素放到最后
    }

    return index1 - index2;
  }
}
</script>
