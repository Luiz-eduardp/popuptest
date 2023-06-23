<template>
  <div class="slot-machine">
    <div class="reels">
      <div class="reel" v-for="reel in reels" :key="reel.id">
        <div class="symbol-container">
          <div
            class="symbol"
            v-for="symbol in reel.symbols"
            :key="symbol.id"
            :class="{ spin: symbol.spinning }"
            @transitionend="onTransitionEnd(reel.id, symbol.id)"
          >
            {{ symbol.value }}
          </div>
        </div>
      </div>
    </div>

    <q-btn
      @click="spin"
      :disabled="spinning"
      padding="xl"
      color="dark"
      round
      icon="keyboard_double_arrow_up"
    />

    <div
      class="overlay notification"
      v-if="showOverlay"
      @click="dismissOverlay"
    >
      {{ overlayText }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      reels: [
        {
          id: 1,
          symbols: [
            { id: 1, value: "favorite", spinning: false },
            { id: 2, value: "Lemon", spinning: false },
            { id: 3, value: "Orange", spinning: false },
          ],
        },
        {
          id: 2,
          symbols: [
            { id: 4, value: "Orange", spinning: false },
            { id: 5, value: "favorite", spinning: false },
            { id: 6, value: "Lemon", spinning: false },
          ],
        },
        {
          id: 3,
          symbols: [
            { id: 7, value: "Lemon", spinning: false },
            { id: 8, value: "Orange", spinning: false },
            { id: 9, value: "favorite", spinning: false },
          ],
        },
      ],
      spinning: false,
      showOverlay: false,
      overlayText: "",
    };
  },
  methods: {
    spin() {
      this.spinning = true;

      setTimeout(() => {
        this.reels.forEach((reel) => {
          reel.symbols.forEach((symbol) => {
            symbol.spinning = true;
          });
        });

        setTimeout(() => {
          this.reels.forEach((reel) => {
            reel.symbols.forEach((symbol) => {
              this.updateSymbolValue(symbol);
              symbol.spinning = false;
            });
          });

          setTimeout(() => {
            this.spinning = false;
            this.checkVictory();
          }, 500);
        }, 2000);
      }, 100);
    },
    updateSymbolValue(symbol) {
      const symbols = ["Cherry", "Lemon", "Orange"];
      const currentIndex = symbols.indexOf(symbol.value);
      const newIndex = (currentIndex + 1) % symbols.length;
      symbol.value = symbols[newIndex];
    },
    getRandomSymbolValue() {
      const symbols = ["Cherry", "Lemon", "Orange"];
      return symbols[Math.floor(Math.random() * symbols.length)];
    },
    onTransitionEnd(reelId, symbolId) {
      const reel = this.reels.find((r) => r.id === reelId);
      const symbol = reel.symbols.find((s) => s.id === symbolId);
      symbol.spinning = false;
    },
    checkVictory() {
      const middleColumnSymbols = this.reels.map(
        (reel) => reel.symbols[1].value
      );
      const symbolValue = middleColumnSymbols[0];

      if (
        middleColumnSymbols[0] === symbolValue &&
        middleColumnSymbols[1] === symbolValue &&
        middleColumnSymbols[2] === symbolValue
      ) {
        this.showOverlay = true;
        this.overlayText = "Você venceu!";
      } else {
        this.showOverlay = true;
        this.overlayText = "Você perdeu, mas não desista e tente novamente!";
      }
    },
    dismissOverlay() {
      this.showOverlay = false;
    },
  },
};
</script>
