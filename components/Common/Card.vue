<template>
  <v-card class="mx-auto mb-4" outlined>
    <v-img :src="itemData.img_src" :lazy-src="loadingImageSrc" :aspect-ratio="itemData.ratio" class="white--text align-end" gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)">
      <template #placeholder>
        <v-row class="fill-height ma-0" align="center" justify="center">
          <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
        </v-row>
      </template>
      <v-card-title>
        <v-avatar size="48">
          <img alt="user" src="https://cdn.pixabay.com/photo/2020/06/24/19/12/cabbage-5337431_1280.jpg">
        </v-avatar>
        <p class="ml-2 mt-4">John Doe</p>
      </v-card-title>
    </v-img>
  </v-card>
</template>

<script>
export default {
  name: "Card",
  props:{
    itemData: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    loadingImageSrc: 'https://lorempixel.com/30/20/people/1',
    loading: false,
    selection: 1,
  }),
  methods: {
    reserve () {
      this.loading = true
      setTimeout(() => (this.loading = false), 2000)
    },
  },
}
</script>

<style scoped>

</style>
