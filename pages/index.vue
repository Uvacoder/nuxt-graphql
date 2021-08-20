<template>
  <v-main>
    <Banner :image-props="bannerImage" :loading-image-props="bannerLoadingImage"/>
    <WhyUs/>
    <Banner :image-props="featureImage" :loading-image-props="bannerLoadingImage"/>
    <Showcase/>
    <v-container>
      <v-row>
        <v-col cols="12">
          <Masonry/>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>
<script>
import Banner from "~/components/Common/Banner";
import WhyUs from "~/components/Index/WhyUs";
import Showcase from "~/components/Index/Showcase";
import Masonry from "~/components/Common/Masonry";

export default {
  components: {Masonry, Showcase, WhyUs, Banner},
  data: () => ({
    bannerImage : 'https://lorempixel.com/1920/760/nature',
    bannerLoadingImage : 'https://lorempixel.com/300/200/nature',
    featureImage : 'https://lorempixel.com/1920/400/people',
    isActive: {
      whyUs : false,
      showCase: false
    },
  }),
}
</script>
