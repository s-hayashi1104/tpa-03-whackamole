<template>
  <div :class="{ 'moles-container': isActive }">
      <Mole v-for='mole in moles' :key="mole"></Mole>
  </div>
</template>

<script>
import Mole from './Mole';
export default {
  name: 'Moles',
  props: {
    moles: 'moles',
    isActive: 'gameActive',
  },
  components: {
    Mole,
  }
};
</script>
   

<style>
.moles-container {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  opacity: 0.5;
  transition: opacity 0.3s ease;
}

.moles-container.game-active {
  opacity: 1;
}
</style>
