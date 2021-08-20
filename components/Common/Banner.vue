<template>
  <v-img :src="imageProps" :lazy-src="loadingImageProps">
    <template #placeholder>
      <v-row class="fill-height ma-0" align="center" justify="center">
        <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
      </v-row>
    </template>
  </v-img>
</template>

<script>
export default {
  name: "Banner",
  props: {
    imageProps: {
      type: String,
      default: null,
      required: true
    },
    loadingImageProps: {
      type: String,
      default: null,
      required: true
    }
  }
}
</script>
