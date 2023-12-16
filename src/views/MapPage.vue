<template>
  <v-main class="pa-0 ma-0">
    <v-container fluid class="my-10">
      <v-row>
        <v-col md="12" sm="12" cols="12" class="text-center  google-font">
          <p
            class="google-font gdg-h1 mb-2 grey--text text--darken-4"
            style="font-size: 220%"
          >
            Map
          </p>
          <p>
            Navigate through the event with these maps
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12" md="6" sm="12">
          <v-img
            style="border-radius: 15px"
            :src="require('@/assets/img/common/map1.jpg')"
          ></v-img>
        </v-col>
        <v-col cols="12" md="6" sm="12">
          <v-img
            style="border-radius: 15px"
            :src="require('@/assets/img/common/map4.jpg')"
          ></v-img>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>

export default {
  name: "MapPage"
};
</script>

<style>
</style>