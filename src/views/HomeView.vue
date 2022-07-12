<template>
  <div class="flex flex-col h-screen bg-gray-900 text-gray-300">
    <HeaderComponent />
    <SectionComponent />    
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HeaderComponent from '@/components/HeaderComponent.vue';
import SectionComponent from '@/components/SectionComponent.vue';

export default defineComponent({
  name: 'HomeView',
  components: {
    HeaderComponent,
    SectionComponent,    
  },
});
</script>
