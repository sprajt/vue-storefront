<template>
  <div class="overlay" @click="onClick" v-if="isVisible">
  </div>
</template>

<script>
import EventBus from 'src/event-bus/event-bus'

export default {
  name: 'overlay',
  data () {
    return {
      isVisible: false
    }
  },
  created () {
    const self = this
    EventBus.$on('toggle-overlay', () => {
      self.isVisible = !self.isVisible
    })
    EventBus.$on('hide-overlay', () => {
      self.isVisible = false
    })
  },
  methods: {
    onClick () {
      EventBus.$emit('hide-overlay')
      EventBus.$emit('hide-sidebar-menu')
      EventBus.$emit('hide-microcart')
    }
  }
}
</script>

<style scoped>
.overlay {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    background: rgba(0,0,0,.4);
    z-index: 1;
}
</style>