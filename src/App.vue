<template>
  <div class="container">
    <timer v-for="(item, index) in timers" :key="index" />
    <div @click="add" class="add">
      <img src="@/assets/grave.svg" />
    </div>
  </div>
</template>

<script>
import timer from "@/components/timeTimer.vue";

export default {
  components: {
    timer,
  },
  data() {
    return {
      timers: 2,
    };
  },
  methods: {
    add() {
      this.timers++;
    },
  },
};
</script>

<style>
body {
  background-color: #353638;
  transition: all 0.3s;
  box-sizing: border-box;
}
.container {
  max-width: 800px;
  padding: 0 25px;
  margin: 0 auto;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(auto-fit, 225px);
  grid-column-gap: 50px;
  grid-row-gap: 45px;
}
.add {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 120px;
  width: 100%;
  background-color: #696969;
}
</style>
