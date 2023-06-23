<template>
  <div class="popup">
    <button class="popup__close-button popupBox" @click="closePopup">
      Fechar
    </button>
    <h2>{{ config.title }}</h2>
    <h3>{{ config.subtitle }}</h3>
    <div class="container">
      <div v-if="showImage" class="item">
        <!-- Exibir imagem aqui -->
        <img
          class="slotImage"
          src="../assets/caca-niquel-image.png"
          alt="joguinho"
        />
      </div>

      <div v-else class="item"><slotMachine /></div>
      <div class="item">
        <form>
          <div
            v-for="(field, index) in config.formFields"
            :key="index"
            class="form-field"
          >
            <q-input
              class="input"
              standout
              v-model="text"
              :label="getFieldLabel(field)"
              :placeholder="getFieldPlaceholder(field)"
            />
          </div>
          <div v-if="config.consentCheckbox" class="form-field">
            <q-checkbox
              v-model="consentChecked"
              label="Consentimento para coleta de dados"
            />
          </div>
          <q-btn
            :ripple="{ center: true }"
            color="secondary"
            label="Enviar"
            no-caps
          />
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import slotMachine from "../components/SlotMachine.vue";

export default {
  props: {
    config: {
      type: Object,
      required: true,
    },
  },
  components: {
    slotMachine,
  },
  data() {
    return {
      consentChecked: false,
      showImage: false,
    };
  },
  mounted() {
    if (this.config.content === "image") {
      this.showImage = true;
    }
  },

  methods: {
    getFieldLabel(field) {
      // Mapear o campo para um rótulo legível
      // Pode ser personalizado conforme necessário
      if (field === "email") {
        return "Email:";
      } else if (field === "nome") {
        return "Nome:";
      } else if (field === "número de celular") {
        return "Número de Celular:";
      } else if (field === "gênero") {
        return "Gênero:";
      }
    },
    getFieldPlaceholder(field) {
      // Mapear o campo para um placeholder adequado
      // Pode ser personalizado conforme necessário
      if (field === "email") {
        return "Digite seu email";
      } else if (field === "nome") {
        return "Digite seu nome";
      } else if (field === "número de celular") {
        return "Digite seu número de celular";
      } else if (field === "gênero") {
        return "Selecione seu gênero";
      }
    },
  },
};
</script>
