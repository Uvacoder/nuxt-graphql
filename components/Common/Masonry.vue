<template>
    <vue-masonry-wall :items="items" :options="{width: 300, padding: 12}" :ssr="{columns: 3}" @append="append">
      <template #default="{item}">
        <Card :item-data="item"/>
      </template>
    </vue-masonry-wall>
</template>

<script>
import VueMasonryWall from "vue-masonry-wall";
import Card from "~/components/Common/Card";

export default {
  name: "Masonry",
  components: {Card, VueMasonryWall},
  data() {
    return {
      items: [
        {
          img_src: 'https://lorempixel.com/300/200/people',
          owner: 'Abc Xyz',
          ratio: 3/2
        },
        {
          img_src: 'https://lorempixel.com/300/400/people',
          owner: 'Xyz Abc',
          ratio: 3/4
        }
      ]
    }
  },
  methods: {
    /**
     * I am mocking a API call that load 20 objects at a time.
     */
    append() {
      // eslint-disable-next-line prefer-const
      for (let i = 0; i < 20; i++) {
        const imgHeight = this.getRndInteger(200, 400);
        this.items.push(
          {
            img_src: 'https://lorempixel.com/300/'+ imgHeight +'/people',
            owner: 'Abc Xyz',
            ratio: 300/imgHeight
          }
        )
      }
    },
    getRndInteger(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    }
  }
}
</script>

<style scoped>

</style>
