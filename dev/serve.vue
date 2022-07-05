<template>
  <div id="app">
    <PackageName />
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import PackageName from '@/package-name.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    PackageName
  }
});
</script>
