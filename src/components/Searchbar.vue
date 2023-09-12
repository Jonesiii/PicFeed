

<template>
  <div>
    <input type="text" placeholder="Search for pics..." v-model="query" />
    <button @click.prevent="emitSearch">Search</button>
  </div>
  
  <button class="randomButton" @click.prevent="emitRandom">Random</button>
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
        this.resetSearchField();
      },

    }
  }
</script>
