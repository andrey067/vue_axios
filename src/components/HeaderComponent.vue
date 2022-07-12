<template>
  <div>
    <header class="border-b border-gray-800">
      <div class="container p-4 mx-auto text-center">
        <h1 class="font-medium text-xl">Axios</h1>
      </div>
    </header>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import '@/assets/tailwind.css';
export default defineComponent({
  name: 'HomePage',

});
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
