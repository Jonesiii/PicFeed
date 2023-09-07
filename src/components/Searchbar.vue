

<template>
  <div>
    <input type="text" placeholder="Search for pics..." v-model="query" />
    <button @click.prevent="emitSearch">Search</button>
  </div>
  
  <button class="randomButton" @click.prevent="emitRandom">Random</button>
  <button class="randomButton" @click.prevent="emitFeed">Feed</button>
</template>

<script>
  export default {
    data () {
      return {
        query: ""
      }
    },
    methods: {
      resetSearchField() {
        this.query = "";
      },
      emitRandom() {
        console.log('clicked');
        this.$emit('random');
      },
      emitSearch() {
        console.log(`searched with ${this.query}`);
        this.$emit('search', this.query);
      },
      emitFeed() {
        console.log('feeded');
        this.$emit('feed');
      }
    }
  }
</script>
