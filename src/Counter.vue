<template>
  <div id="app">
    <span ref="counter">{{ getCount }}</span>
    <br>
    <input type="button" value="inc" @click="increment">
    <input type="button" value="dec" @click="decrement">
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

import Velocity from 'velocity-animate';

export default {
  computed: mapGetters([
    'getCount',
  ]),
  methods: {
    async increment() {
      // 1. stop all animation queues
      await Velocity(this.$refs.counter, 'stop');
      // 2. fade-out counter
      await Velocity(this.$refs.counter, 'fadeOut', { duration: 250 });
      // 3. update store
      await this.$store.dispatch('increment');
      // 4. fade-in counter
      await Velocity(this.$refs.counter, 'fadeIn', { duration: 250 });
    },
    async decrement() {
      await Velocity(this.$refs.counter, 'stop');
      await Velocity(this.$refs.counter, 'fadeOut', { duration: 250 });
      await this.$store.dispatch('decrement');
      await Velocity(this.$refs.counter, 'fadeIn', { duration: 250 });
    },
  },
};
</script>
