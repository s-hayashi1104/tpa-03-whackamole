<template>
  <div :class="handleContainer">
    <template v-for='(moleActive, index) in moles' >
      <Mole :key="index" :moleId="index" :active="moleActive" @whack="handleWhack"></Mole>
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
        'moles-container': true ,
        'game-active': this.isActive,
      };
    }
  },
  methods: {
    handleWhack: function(moleId) {
      this.$emit('whack', moleId);
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
