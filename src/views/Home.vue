<template>
  <div class="home">
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
