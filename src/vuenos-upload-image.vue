<template>
  <!--upload img-->
  <div v-if="type === 'upload'" class="image-frame">
    <div class="image-item" :style="{width: propsWidth || '75px', height: (propsWidth/3) || '85px'}" v-for="(img, index) in imageList" :key="index">
      <div class="image-src" :style="{backgroundImage: `url(${img})`}"></div>
      <svg xmlns="http://www.w3.org/2000/svg" :width="(propsWidth/10) || 24" :height="(propsWidth/10) || 24" fill="currentColor"
           class="bi bi-trash remove-overlay" @click="removeImage(index)"
           viewBox="0 0 16 16">
        <path
            d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
        <path fill-rule="evenodd"
              d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
      </svg>
    </div>
    <div class="add-img" :style="{width: propsWidth || '75px', height: (propsWidth/3) || '85px'}" v-if="imageList.length < (maxImages || 9999)">
      <label for="img">
        <svg xmlns="http://www.w3.org/2000/svg" :width="(propsWidth/10) || 24" :height="(propsWidth/10) || 24" fill="currentColor"
             class="bi bi-zoom-in"
             viewBox="0 0 16 16">
          <path fill-rule="evenodd"
                d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>
          <path
              d="M10.344 11.742c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1 6.538 6.538 0 0 1-1.398 1.4z"/>
          <path fill-rule="evenodd"
                d="M6.5 3a.5.5 0 0 1 .5.5V6h2.5a.5.5 0 0 1 0 1H7v2.5a.5.5 0 0 1-1 0V7H3.5a.5.5 0 0 1 0-1H6V3.5a.5.5 0 0 1 .5-.5z"/>
        </svg>
      </label>
      <input v-on:change="onFileChange" :disabled="propsDisabled" style="display: none;" type="file" id="img" name="img"
             multiple
             :accept="propsImageTypes"/>
    </div>
  </div>

  <!--show image-->
  <!--  <div v-else-if="type === 'preview'" class="image-frame">-->
  <!--    <div class="image-item" v-for="(path, index) in imgListPreview" :key="index"-->
  <!--         @click="openImgDialog(`${STORE_IMAGE}/${path}`)">-->
  <!--      <div class="image-src" :style="{backgroundImage: urlBackground(path)}"></div>-->
  <!--      <div class="img-hover-cover">-->
  <!--        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-zoom-in"-->
  <!--             viewBox="0 0 16 16">-->
  <!--          <path fill-rule="evenodd"-->
  <!--                d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>-->
  <!--          <path-->
  <!--              d="M10.344 11.742c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1 6.538 6.538 0 0 1-1.398 1.4z"/>-->
  <!--          <path fill-rule="evenodd"-->
  <!--                d="M6.5 3a.5.5 0 0 1 .5.5V6h2.5a.5.5 0 0 1 0 1H7v2.5a.5.5 0 0 1-1 0V7H3.5a.5.5 0 0 1 0-1H6V3.5a.5.5 0 0 1 .5-.5z"/>-->
  <!--        </svg>-->
  <!--      </div>-->
  <!--    </div>-->
  <!--    <el-dialog v-model="imgDialog"-->
  <!--               width="30%"-->
  <!--               center-->
  <!--               append-to-body>-->
  <!--      <img class="width100" :src="imgDialogSource" alt="">-->
  <!--    </el-dialog>-->
  <!--  </div>-->
</template>
<script>
import {computed, ref} from "vue";

export default {
  emits: ['getImgFileList'],
  props: ['imgListPreview', 'type', 'disabled', 'width', 'maxImages', 'imageTypes', 'maxSize'],

  setup(props, {emit}) {
    const STORE_IMAGE = process.env.STORE_IMAGE || ''

    const propsDisabled = computed(() => {
      return props.disabled || false
    })
    const propsWidth = computed(() => {
      return props.width ? props.width.toString() + 'px' : '75px'
    })
    const propsImageTypes = computed(() => {
      return props.imageTypes || 'image/*'
    })

    const urlBackground = (path) => {
      const url = 'url(' + STORE_IMAGE + path.replace('(', '%28').replace(')', '%29').replace(' ', '%20') + ')'
      return url
    }

    /**
     * Upload image
     */
    const imgFileList = ref([])
    const imageList = ref([])

    const createImage = (file) => {
      let image = new Image();
      const reader = new FileReader();

      reader.readAsDataURL(file);

      reader.onload = (e) => {
        image = e.target.result;
        imageList.value.push(image)
      };
    }

    const removeImage = (index) => {
      if (propsDisabled.value === true) return;
      imageList.value.splice(index, 1)
      imgFileList.value.splice(index, 1)
    }

    const onFileChange = (e) => {
      // đẩy dữ liệu vào array
      let files = []
      files.push(...e.target.files || e.dataTransfer.files);

      // check length dữ liệu (bs: tối đa maxImages ảnh)
      if (!files.length || files.length > props.maxImages || imageList.value.length > props.maxImages || (files.length + imageList.value.length) > props.maxImages) return;

      // filter loại ảnh
      files = files.filter(file => {
        return file.type === "image/jpg" ||
            file.type === "image/jpeg" ||
            file.type === "image/png" ||
            file.size <= props.maxSize || 8000000 // check dung lượng ảnh (bs: tối đa mỗi ảnh là maxSize hoặc 8mb)
      });

      // hiển thị ảnh
      for (let i = 0; i < files.length; i++) {
        createImage(files[i])
        imgFileList.value.push(files[i])
      }
      emit('getImgFileList', imgFileList.value)
    }

    /**
     * Show image
     */
    const imgDialog = ref(false)
    const imgDialogSource = ref(null)

    const openImgDialog = async (url) => {
      imgDialog.value = true
      imgDialogSource.value = url
    }

    return {
      STORE_IMAGE,
      imageList,
      imgDialog,
      imgDialogSource,
      propsDisabled,
      propsWidth,
      propsImageTypes,
      removeImage,
      onFileChange,
      openImgDialog,
      urlBackground
    }
  }
}
</script>
<style scoped lang="scss">
.image-frame {
  display: flex;
  gap: 5px;
  width: max-content;

  .image-item {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    border: 1px solid #A1A5B7;
    border-radius: 4px;
    padding: 1px;
    cursor: pointer;
    height: 100%;

    &:hover {
      border: 1px solid rgb(64, 158, 255);

      i {
        color: rgb(64, 158, 255);
      }

      .remove-overlay {
        opacity: 1;
      }

      .image-src {
        opacity: 0.2;
      }

      .img-hover-cover {
        opacity: 1;

        .el-icon, svg {
          width: 2rem;
          height: 2rem;
        }
      }
    }

    .image-src {
      height: 100%;
      width: 100%;
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
    }

    .img-hover-cover {
      position: absolute;
      z-index: 1;
      opacity: 0;
    }

    .remove-overlay {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      opacity: 0;
      transition: .3s ease;
      cursor: pointer;
    }
  }

  .add-img {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 75px;
    border: 2px dashed #A1A5B7;
    border-radius: 4px;
    //transition: all 0.15s linear;
    color: #A1A5B7;

    &:hover {
      border: 2px dashed rgb(64, 158, 255);

      label {
        color: rgb(64, 158, 255);
      }
    }

    label {
      display: flex;
      justify-content: center;
      align-items: center;

      width: 100%;
      height: 100%;

      cursor: pointer;
    }
  }

  img {
    max-width: 100%;
    transition: .3s ease;
  }
}
</style>