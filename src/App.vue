<template>
  <TimerComponent />
</template>

<script>
import TimerComponent from "./components/Timer.vue";

export default {
  name: "App",
  components: {
    TimerComponent,
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
