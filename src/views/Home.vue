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
    const searchParams: any = new URLSearchParams(location.search);
    for(var key of searchParams.keys()) {
      this.options.push({
        key,
        value: searchParams.get(key)
      })
    }
  }
}
</script>
