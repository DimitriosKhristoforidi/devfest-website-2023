<template>
  <v-container fluid class="pa-0 ma-0" v-if="data" style="height: 100%;">
    <v-row
      justify="center"
      align="center"
      class="d-none d-md-flex pa-0 my-0 row-border-white"
    >
      <v-col md="2" cols="12" class="text-left text-md-right my-0 py-0" />
      <v-col
        v-for="(room, index) in roomsData "
        :key="index"
        class="my-0 schedule-details-white col-border-white"
        cols="12"
        :md="3"
      >
        {{ room.name }}
      </v-col>
    </v-row>
    <v-row
      justify="center"
      align="center"
      v-for="(item, index) in data['schedule']"
      :key="index"
      class="pa-0 my-0 row-border-white"
    >
      <v-col md="2" cols="12" class="d-flex flex-column justify-center text-left text-md-right mt-6 mt-md-0">
        <p class="mx-4 mx-md-0 mb-0 google-font" style="font-size: 110%" >
          {{ item.startTime }}
        </p>
        <p class="mx-4 mx-md-0 ma-0 google-font" style="font-size: 70%" >
          {{ item.endTime }}
        </p>
        <p class="mx-4 mx-md-0 mt-1 google-font" style="font-size: 60%">
          <b style="color: grey">GMT+6</b>
        </p>
      </v-col>
      <v-col
        v-for="(session, indexp) in item['sessions']"
        :key="indexp"
        class="my-0 schedule-details-white col-border-white"
        cols="12"
        :md="Math.floor(10 / item['sessions'].length)"
      >
        <scheduleDialog :data="getSessionData(session)" />
      </v-col>
    </v-row>
  </v-container>
</template>
  
  <script>
import scheduleDialog from "@/components/schedule/scheduleDialog";
import sessionsJSON from "@/assets/data/sessions.json";
import roomsJSON from "@/assets/data/rooms.json";
export default {
  props: ["data"],
  components: {
    scheduleDialog,
  },
  data: () => ({
    sessionsInfo: sessionsJSON,
    roomsData: roomsJSON
  }),
  methods: {
    getSessionData(id) {
      return this.sessionsInfo.find((sd) => sd.id === id);
    },
  },
};
</script>
  
  <style scoped>
.schedule-details-white:hover {
  background: #fafafa;
}
.row-border-white {
  border-bottom: 1px solid #e0e0e0;
  align-items: stretch !important;;
}
.col-border-white {
  border-left: 1px solid #e0e0e0;
}
</style>