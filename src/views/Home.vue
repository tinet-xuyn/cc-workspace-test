<template>
  <div class="home">
      <h1>呼叫工作台自定义弹屏参数专用测试页面</h1>
      <div v-for="item in options" :key="item.id">
        {{ item.key }}: {{ item.value }}
      </div>
  </div>
</template>

<script lang="ts">
import { reactive } from 'vue';
import { Vue } from 'vue-class-component';
export default class Home extends Vue {
 options: any = reactive([]);

  created() {
    const obj = this.$route.query
    for (const key in obj) {
      this.options.push({
        key,
        value: obj[key]
      })
    }
  }
}
</script>
