<template>
  <v-dialog v-if="data" v-model="dialog" width="800" scrollable>
    <template v-slot:activator="{ on }">
      <div
        v-on="on"
        style="cursor: pointer"
        class="py-3 px-3 px-md-0 ma-1 fill-height"
      >
        <span v-if="data.room !== undefined">
          <v-chip class="mb-2 d-md-none" outlined small>
            {{ getRoomName(data.room) }}
          </v-chip>
        </span>
        <p class="mb-0 h1-subheading google-font">{{ data.title }}</p>

        <span v-for="(itemp, indexp) in speakers" :key="indexp">
          <v-chip pill class="mt-2 mr-2" outlined>
            <v-avatar left>
              <img :src="getImgUrl(itemp.image)" class="image-wrapper" />
            </v-avatar>
            {{ itemp.name }}
          </v-chip>
        </span>

        <v-chip v-if="data.track" small class="mt-2">{{ data.track }}</v-chip>
      </div>
    </template>

    <v-card class="pa-0 white" v-if="dialog" style="border-radius: 12px">
      <iframe
        v-if="data.link"
        class="ma-0 pa-0"
        width="100%"
        height="415"
        style="border: none"
        :src="data.link"
      >
      </iframe>
      <v-card-text class="px-5 google-font mt-n0 pt-5 pb-0">
        <v-container fluid>
          <v-row>
            <v-col md="12" cols="12">
              <p
                class="my-3 mb-5 font-weight-medium text-black"
                style="font-size: 25px; line-height: 25px"
              >
                {{ data.title }}
              </p>
              <p v-if="data.date.length" class="mb-1">
                <v-icon small>mdi-calendar-month</v-icon>
                {{ data.date }}
              </p>

              <p v-if="data.startTime" class="mb-1">
                <v-icon small>mdi-clock-outline</v-icon>
                {{ data.startTime }} to {{ data.endTime }} (GMT+6)
              </p>

              <p v-if="data.room" class="mb-1">
                <v-icon small>mdi-map-marker</v-icon>
                {{ getRoomName(data.room) }}
              </p>

              <p class="mb-1">{{ data.timeDuration }} Min</p>

              <p
                v-if="data.description"
                class="mt-10 font-weight-medium"
                style="font-size: 22px; color: black"
              >
                Overview
              </p>
              <p style="font-size: 105%; color: black; opacity: 0.9">
                {{ data.description }}
              </p>

              <!-- <v-chip small pill>{{ data.format }}</v-chip> -->
              <v-chip v-if="data.track" small class="mt-2">{{
                data.track
              }}</v-chip>

              <v-chip
                v-if="data.slide"
                :href="data.slide"
                color="indigo"
                outlined
                target="_blank"
                class="mt-2 mr-2"
                label
              >
                <v-avatar left>
                  <v-icon small>mdi-note-outline</v-icon>
                </v-avatar>
                Presentation
              </v-chip>
              <v-container fluid class="px-0 mx-0">
                <v-row
                  class="pa-0 ma-0"
                  v-for="(itemp, indexp) in speakers"
                  :key="indexp"
                >
                  <v-col class="pa-0 ma-0">
                    <v-list two-line subheader class="pa-0 ma-0 white">
                      <v-list-item class="my-0 py-0">
                        <v-list-item-avatar size="50">
                          <img
                            :src="getImgUrl(itemp.image)"
                            class="image-wrapper"
                          />
                        </v-list-item-avatar>
                        <v-list-item-content>
                          <v-list-item-title
                            class="google-font"
                            style="font-size: 150%; font-weight: 500"
                            >{{ itemp.name }}</v-list-item-title
                          >
                          <v-list-item-subtitle
                            class="google-font text-wrap"
                            style="font-size: 105%"
                          >
                            {{ itemp.company?.name }}
                          </v-list-item-subtitle>
                        </v-list-item-content>
                      </v-list-item>
                    </v-list>
                  </v-col>
                </v-row>
              </v-container>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import speakersJSON from "@/assets/data/speakers.json";
import roomsJSON from "@/assets/data/rooms.json";
export default {
  components: {},
  props: ["data"],
  data() {
    return {
      dialog: false,
      speakersInfo: speakersJSON,
      roomsInfo: roomsJSON,
      speakers: [],
    };
  },
  mounted() {
    this.speakers = [];
    if (this.data)
      this.speakers = this.data.speakers?.map((item) =>
        this.speakersInfo.find((speaker) => speaker.id === item)
      );
  },
  methods: {
    getImgUrl(pic, defaultimage = "avatar.jpg") {
      if (pic.length > 0) {
        return require("@/assets/img/speakers/" + pic);
      } else {
        return require("@/assets/img/common/" + defaultimage);
      }
    },
    getRoomName(id) {
      return this.roomsInfo?.find((room) => room.id === id)?.name;
    },
  },
  filters: {
    summary: (val, num) => {
      if (val.length > num) return val.substring(0, num) + "..";
      else return val;
    },
  },
};
</script>
<style scoped>
.image-wrapper {
  object-fit: cover;
  object-position: center;
}
</style>
