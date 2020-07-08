<template>
  <div id="app">
    <div class="container">
      <v-outlined-textfield v-model="myData"></v-outlined-textfield>
    </div>
  </div>
</template>

<script>
import vOutlinedTextfield from '@/components/OutlinedTextfield.vue';

export default {
  data() {
    return {
      myData: 'Test Data'
    }
  },
  components: {
    vOutlinedTextfield
  }
}
</script>

<style>
body {
  background-color: #fff;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: inherit;
}

.container {
  background-color: inherit;
  width: 400px;
  margin: 0 auto;
}
</style>
