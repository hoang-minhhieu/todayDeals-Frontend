<style>
.q-carousel {
  margin-left: 8px;
}
</style>

<template>
  <q-carousel
    v-model="slide"
    swipeable
    animated
    control-color="purple"
    navigation
    padding
    arrows
    height="250px"
    class="text-purple rounded-borders"
  >
    <q-carousel-slide name="style" class="column no-wrap flex-center">
      <q-icon name="style" size="56px" />
      <div class="q-mt-md text-center text-black">
        {{ lorem }}
      </div>
    </q-carousel-slide>
    <q-carousel-slide name="tv" class="column no-wrap flex-center">
      <q-icon name="live_tv" size="56px" />
      <div class="q-mt-md text-center text-black">
        {{ lorem }}
      </div>
    </q-carousel-slide>
    <q-carousel-slide name="layers" class="column no-wrap flex-center">
      <q-icon name="layers" size="56px" />
      <div class="q-mt-md text-center text-black">
        {{ lorem }}
      </div>
    </q-carousel-slide>
  </q-carousel>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
export default defineComponent({
  name: 'HighlightComponent',
  setup() {
    return {
      slide: ref('style'),
      lorem:
        'Lorem ipsum dolor, sit amet consectetur adipisicing elit. Itaque voluptatem totam, architecto cupiditate officia rerum, error dignissimos praesentium libero ab nemo.',
    };
  },
});
</script>
