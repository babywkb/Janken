<template>
  <div class="root">
    <p>じゃんけん……</p>
    <p>
      <HandButton :phase="{phase}" :janken="this.janken" :hand='GU'/>
      <HandButton :phase="{phase}" :janken="this.janken" :hand='CHOKI'/>
      <HandButton :phase="{phase}" :janken="this.janken" :hand="PA"/>
      <button class="reset-button" :disabled="false" @click:="reset">もう一回</button>
    </p>
    <p v-if="this.phase === 'INIT'">ぽん！</p>
    <div v-if="this.phase === 'FINISHED'">
      <p class="hand">
        あなたは
        <span>{{hands[player]}}</span>
      </p>
      <p class="hand">
        相手は
        <span>{{hands[enemy]}}</span>
      </p>
      <p class="issue">{{issues[issue]}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Janken",
  props: {
    msg: String
  },
  beforeMount: function() {
    this.setPhase("INIT");
    this.setPlayer("GU");
    this.setEnemy("GU");
    this.setIssue("DRAW");
  },
  methods: {
    janken: async hand => {
      this.setPhase("STARTED");
      const headers = { "Content-Type": "application/json" };
      const body = JSON.stringify({ player: hand });
      const res = await fetch("/api/janken", { method: "POST", headers, body });
      const { player, enemy, issue } = await res.json();
      this.setPhase("FINISHED");
      this.setPlayer(player);
      this.setEnemy(enemy);
      this.setIssue(issue);
    },
    activate: function() {
      if (this.phase !== "FINISHED") {
        return true;
      } else {
        return false;
      }
    },
    setPhase: function(phase) {
      this.phase = phase;
    },
    setPlayer: function(player) {
      this.player = player;
    },
    setEnemy: function(enemy) {
      this.enemy = enemy;
    },
    setIssue: function(issue) {
      this.issue = issue;
    },
    reset: function() {
      this.etPhase("INIT");
    }
  },
  data() {
    return {
      phase: "",
      player: "",
      enemy: "",
      issue: "",
      hands: {
        GU: "✊",
        CHOKI: "✌️",
        PA: "🖐"
      },
      issues: {
        WIN: "😄勝ち",
        DRAW: "🤔あいこ",
        LOSE: "😣負け"
      }
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
