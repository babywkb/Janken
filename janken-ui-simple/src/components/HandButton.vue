<template>
  <div class="hand-button">
    <button @click="jankenChild(hand)" :disabled="phase !== 'INIT'">{{hands[hand]}}</button>
  </div>
</template>

<script>
export default {
  name: "HandButton",
  props: ["hand", "phase"],
  methods: {
    jankenChild: function(hand) {
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