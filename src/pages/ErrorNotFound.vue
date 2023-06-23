<template>
  <div
    class="fullscreen bg-grey text-white text-center q-pa-md flex flex-center"
  >
    <div>
      <div style="font-size: 30vh">404</div>

      <div class="text-h2 page404">
        Oops. acho que isso não foi implementado...
      </div>

      <q-btn
        class="q-mt-xl"
        color="green"
        text-color="white"
        elevated
        to="/"
        label="Voltar"
      />
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "ErrorNotFound",
});
</script>
