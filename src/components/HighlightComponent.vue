<style scoped lang="scss">
.q-carousel {
  margin: 8px 0 5px 3px;
  height: 150px;
}

.carousel-card {
  display: flex;
  flex-direction: row;
  flex-shrink: 0;
  width: calc(100% / 5 - 10px);
  .q-card-section {
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    width: calc(100% - 80px);
  }
}

.carousel-container {
  display: flex;
  flex-direction: row;
  gap: 10px;
  width: 100%;
}

.carousel-title {
  align-self: baseline;
  color: red;
  font-size: 1.3rem;
  text-align: center;
  align-items: center;
  display: flex;
}

.carousel-card-image {
  width: 80px;
  height: 80px;
}

.carousel-card-content {
  font-size: 0.8rem;
}
</style>

<template>
  <q-carousel
    v-model="slide"
    swipeable
    animated
    control-color="purple"
    padding
    arrows
    class="rounded-borders"
  >
    <q-carousel-slide name="style" class="column no-wrap flex-center">
      <div class="carousel-title">
        <q-icon name="local_fire_department" />Hot nhất trong ngày
      </div>
      <div class="carousel-container">
        <q-card
          v-for="(item, index) in carouselItems"
          :key="index"
          class="carousel-card"
        >
          <img
            src="https://cdn.quasar.dev/img/parallax2.jpg"
            class="carousel-card-image"
          />
          <q-card-section class="carousel-card-content ellipsis">
            {{ item.description }}
          </q-card-section>
        </q-card>
      </div>
    </q-carousel-slide>

    <q-carousel-slide name="layers" class="column no-wrap flex-center">
      <div class="carousel-title">
        <q-icon name="local_fire_department" />Hot nhất tuần
      </div>
      <div class="carousel-container">
        <q-card
          v-for="(item, index) in carouselItems"
          :key="index"
          class="carousel-card"
        >
          <img
            src="https://cdn.quasar.dev/img/parallax2.jpg"
            class="carousel-card-image"
          />
          <q-card-section class="carousel-card-content ellipsis">
            {{ item.description }}
          </q-card-section>
        </q-card>
      </div>
    </q-carousel-slide>

    <q-carousel-slide name="tv" class="column no-wrap flex-center">
      <div class="carousel-title">
        <q-icon name="local_fire_department" />Hot nhất tháng
      </div>
      <div class="carousel-container">
        <q-card
          v-for="(item, index) in carouselItems"
          :key="index"
          class="carousel-card"
        >
          <img
            src="https://cdn.quasar.dev/img/parallax2.jpg"
            class="carousel-card-image"
          />
          <q-card-section class="carousel-card-content ellipsis">
            {{ item.description }}
          </q-card-section>
        </q-card>
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
      carouselItems: [
        {
          id: 1,
          title: 'Card 1',
          description: 'Rasoir anti-bouloche et anti-peluche Philips GC026/00',
        },
        {
          id: 2,
          title: 'Card 2',
          description:
            'Console Nintendo Switch OLED Pokémon Scarlet et Violet (via 35€ sur la carte de fidélité)',
        },
        {
          id: 3,
          title: 'Card 3',
          description:
            'Carte graphique Sapphire Radeon RX 7900 XT - 20Go (hardwarecamp24.de)',
        },
        { id: 4, title: 'Card 4', description: 'Gilet de sécurité jaune' },
        { id: 5, title: 'Card 5', description: 'This is a description' },
      ],
    };
  },
});
</script>
