<template>
  <v-main class="pa-0 ma-0">
    <!-- Hero -->
    <heroVue class="my-md-5 my-sm-5" />
    <!-- Hero -->

    <!-- Technologies -->
    <technologiesVue class="mt-5"/>
    <!-- Technologies -->

    <!-- Sponsors -->
    <homesponsors class="my-"/>
    <!-- Sponsors -->

    <!-- Social -->
    <homeSocialVue class="my-10"/>
    <!-- Social -->
  </v-main>
</template>

<script>
import heroVue from "@/components/home/hero.vue";
import technologiesVue from '@/components/home/technologies.vue';
import homesponsors from '@/components/home/homeSponsors.vue';
import homeSocialVue from '@/components/home/homeSocial.vue';

export default {
  name: "HomePage",
  components: {
    heroVue,
    technologiesVue,
    homesponsors,
    homeSocialVue
  },
  data: () => ({
    
  }),
};
</script>
