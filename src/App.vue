
<template>
  <div class="container">
    <Timer v-for="timerId in timersArray" :key="timerId" />
    <AddButton :addFunc="addTimer" />
  </div>
</template>


<script>
import Timer from "./components/Timer.vue";
import AddButton from "./components/AddButton.vue";
export default {
  components: {
    Timer,
    AddButton
  },
  data() {
    return {
      timersArray: [1]
    };
  },
  methods: {
    addTimer() {
      this.timersArray.push(this.timersArray[this.timersArray.length - 1] + 1);
    }
  }
};
</script>

<style lang="scss" >

.container {
  padding: 72px 0;
  box-sizing:border-box;
  width: 100%;
  display: grid;
  column-gap: 50px;
  row-gap: 45px;
  grid-template-columns: repeat(3, 1fr);

}
@media (max-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 510px) {
  .container {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
