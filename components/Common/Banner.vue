<template>
  <v-img :src="src" :lazy-src="lazySrc">
    <template v-slot:placeholder>
      <v-row class="fill-height ma-0" align="center" justify="center">
        <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
      </v-row>
    </template>
  </v-img>
</template>

<script>
export default {
  name: "Banner",
  data () {
    return {
      src : 'https://via.placeholder.com/1920x760.png/09f/fff',
      lazySrc : 'https://picsum.photos/id/11/100/60'
    }
  }
}
</script>
