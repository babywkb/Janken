<template>
  <div class="hand-button">
    <button @click="jankenChild(hand)">{{hands[hand]}}</button>
  </div>
</template>

<script>
export default {
  name: "HandButton",
  props: ["hand"],
  methods: {
    jankenChild(hand) {
      this.$emit("call-parent", hand);
    }
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