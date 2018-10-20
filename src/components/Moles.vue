<template>
  <div 
  class="moles-container"
  :class="handleContainer"
  >
    <template v-for='(moleActive, index) in moles' >
      <Mole :key="index" :active="moleActive" @whack="handleWhack(index)"></Mole>
    </template>
  </div>
</template>

<script>
import Mole from './Mole';
export default {
  name: 'Moles',
  props: ['moles', 'isActive'],
  computed: {
    handleContainer: function() {
      return {
        'game-active': this.isActive,
      };
    }
  },
  methods: {
    handleWhack: function(index) {
      this.$emit('whack', index);
    },
  },
  components: {
    Mole,
  }
};
</script>
   

<style lang="scss" scoped>
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
