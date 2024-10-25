<template>
  <v-row class="pa-4">
    <v-col cols="12">
      <!-- New Home Page Notice with bolder and bigger text -->
      <v-card color="blue lighten-3" class="text-center" outlined>
        <v-card-text>
          <h3 class="mb-0" style="font-weight: bold; font-size: 1.5rem; color: black;">Home</h3>
        </v-card-text>
      </v-card>
    </v-col>
    <v-col cols="5" sm="4" md="3" />
    <v-col cols="2" sm="4" md="6" class="text-center">
      <font-awesome-icon
        :icon="statusIcon"
        size="3x"
        :flip="loading"
        :class="{
          'primary--text': loading,
          'secondary--text': !loading && !isDark,
          'accent--text': !loading && isDark,
        }"
      />
    </v-col>
    <v-col cols="5" sm="4" md="3">
      <cong-select-input :disabled="loading || musicPlaying" />
    </v-col>
  </v-row>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import {
  faPhotoVideo,
  faDownload,
  faCloud,
  faGlobeAmericas,
} from '@fortawesome/free-solid-svg-icons'

export default defineComponent({
  props: {
    loading: {
      type: Boolean,
      required: true,
    },
    cong: {
      type: String,
      required: true,
    },
    jw: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      deprecatedShow: true,
      alreadyDeprecated: new Date() >= new Date('2024-11-01'),
    }
  },
  computed: {
    isDark(): boolean {
      return this.$vuetify.theme.dark
    },
    musicPlaying(): boolean {
      return !!this.$store.state.media.musicFadeOut
    },
    statusIcon() {
      if (this.cong === 'warning') {
        return faCloud
      } else if (this.jw === 'warning') {
        return faDownload
      } else if (this.loading) {
        return faGlobeAmericas
      } else {
        return faPhotoVideo
      }
    },
  },
})
</script>