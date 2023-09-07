

<template>
  <input type="text" placeholder="Search for pics..." />
  <button @click.prevent="emitRandom">Random</button>
</template>

<script>
  export default {
    methods: {
      emitRandom() {
        console.log('clicked');
        this.$emit('random');
      }
    }
  }
</script>
