<style>
.my-card {
  width: 100%;
}
</style>

<template>
  <q-infinite-scroll @load="onLoad" :offset="250">
    <div v-for="(item, index) in items" :key="index" class="caption">
      <div class="cards-area">
        <q-card class="my-card" flat bordered>
          <q-card-section horizontal>
            <q-img
              class="col-3"
              src="https://cdn.quasar.dev/img/parallax2.jpg"
            />
            <q-card-section>
              {{ lorem }}
            </q-card-section>
          </q-card-section>
        </q-card>
      </div>
    </div>
    <template v-slot:loading>
      <div class="row justify-center q-my-md">
        <q-spinner-dots color="primary" size="40px" />
      </div>
    </template>
  </q-infinite-scroll>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ref } from 'vue';
export default defineComponent({
  name: 'DealsCardComponent',

  components: {},

  setup() {
    const items = ref([{}, {}, {}, {}, {}, {}, {}]);
    return {
      items,
      onLoad(index: any, done: () => void) {
        setTimeout(() => {
          items.value.push({}, {}, {}, {}, {}, {}, {});
          done();
        }, 2000);
      },
      lorem:
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
    };
  },
});
</script>
