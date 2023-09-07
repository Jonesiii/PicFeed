

<template>
  <div>
    <input type="text" placeholder="Search for pics..." />
    <button @click.prevent="emitSearch">Search</button>
  </div>
  
  <button class="randomButton" @click.prevent="emitRandom">Random</button>
  <button class="randomButton" @click.prevent="emitFeed">Feed</button>
</template>

<script>
  export default {
    methods: {
      emitRandom() {
        console.log('clicked');
        this.$emit('random');
      },
      emitSearch(query) {
        console.log('searched');
        this.$emit('search', 'sunset');
      },
      emitFeed() {
        console.log('feeded');
        this.$emit('feed');
      }
    }
  }
</script>
