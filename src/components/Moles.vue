<template>
  <div :class="{ 'moles-container': isActive }">
    <template v-for='(mole, index) in moles' >
      <Mole :key="index"></Mole>
    </template>
  </div>
</template>

<script>
import Mole from './Mole';
export default {
  name: 'Moles',
  props: ['moles', 'isActive'] ,
  components: {
    Mole,
  }
};
</script>
   

<style lang="scss">
.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.5;
  transition: opacity 0.3s ease;
  &.game-active{
    opacity: 1;
  }
}
</style>
