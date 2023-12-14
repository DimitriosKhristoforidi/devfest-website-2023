<template>
  <div>
    <v-btn v-for="(item, index) in data" :key="index" icon class="mr-1" target="_blank" :href="item?.link">
      <v-icon>mdi-{{ item.type }}</v-icon>
    </v-btn>
  </div>
</template>

<script>
export default {
  props: ["data"],
  data: () => ({}),
};
</script>

<style>
</style>