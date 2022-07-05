<template>
  <div id="app">
    <VuenosUploadImage />
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import VuenosUploadImage from '@/vuenos-upload-image.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    VuenosUploadImage
  }
});
</script>