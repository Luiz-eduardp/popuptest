<template>
  <div class="q-pa-md q-gutter-sm">
    <div class="flex-center">
      <div class="center-content">
        <q-btn
          @click="showGamePopup"
          color="primary"
          label="Abrir Jogo de Caça-níquel"
        />
        <br />
        <br />
        <q-btn @click="showVideoPopup" color="primary" label="Abrir Vídeo" />

        <component
          @click="closePopup"
          class="popupBox"
          :is="currentPopupComponent"
          :config="currentPopupConfig"
          v-if="currentPopupComponent"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import GamePopup from "../components/GamePopup.vue";
import VideoPopup from "../components/VideoPopup.vue";
import popupConfig from "../assets/popupConfig.json";

export default defineComponent({
  name: "IndexPage",
  components: {
    GamePopup,
    VideoPopup,
  },
  data() {
    return {
      currentPopupComponent: null,
      currentPopupConfig: null,
    };
  },
  methods: {
    showGamePopup() {
      this.currentPopupComponent = "GamePopup";
      this.currentPopupConfig = popupConfig["caça-níquel"];
    },
    showVideoPopup() {
      this.currentPopupComponent = "VideoPopup";
      this.currentPopupConfig = popupConfig["vídeo"];
    },
    closePopup(event) {
      if (event.target.classList.contains("popupBox")) {
        this.currentPopupComponent = null;
        this.currentPopupConfig = null;
      }
    },
  },
});
</script>
