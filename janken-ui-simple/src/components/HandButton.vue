<template>
  <div class="hand-button">
    <button @click="janken(hand)" :disabled="false">{{hands[hand]}}</button>
  </div>
</template>

<script>
export default {
  name: "HandButton",
  props: {
    phase: null,
    janken: null,
    hand: null
  },
  data() {
    return {
      hands: {
        GU: "✊",
        CHOKI: "✌️",
        PA: "🖐"
      }
    };
  }
};
</script>