<template>
  <topBanner />
  <cookieArea />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import topBanner from './components/topBanner.vue';
import cookieArea from './components/cookieArea.vue';

export default defineComponent({
  name: 'App',
  components: {
    topBanner,
    cookieArea
  }
});
</script>

