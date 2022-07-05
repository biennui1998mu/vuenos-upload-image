<template>
  <div id="app">
    <vuenos-upload-image :type="'upload'"
                         @getImgFileList="getImgFileList">
    </vuenos-upload-image>
  </div>
</template>
<script lang="ts">
import {defineComponent} from 'vue';
import VuenosUploadImage from '@/vuenos-upload-image.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    VuenosUploadImage
  },
  setup() {
    const getImgFileList = (val: any) => {
      console.log(val)
    }

    return{
      getImgFileList
    }
  }
});
</script>