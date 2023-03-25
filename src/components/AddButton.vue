

<template>
  <div @click="addFunc" class="addButton">
    <img  :src="PlusSvg" alt />
  </div>
</template>

<script>
import PlusSvg from "../assets/images/plus.svg";
export default {
  props: ["addFunc"],
  data() {
    return {
      PlusSvg
    };
  } 
};
</script>

<style lang="scss">
.addButton {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  img{
    opacity: .5;
  }
  &:hover{
    img{
        opacity: 1;
      }
  }
}
</style>