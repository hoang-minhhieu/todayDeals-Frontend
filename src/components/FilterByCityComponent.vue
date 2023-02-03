<template>
  <div>My component</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
const cities = require('../constants/constants');
const provinces = require('../constants/constants');

export default defineComponent({
  name: 'FilterByCityComponent',
  setup() {
    const list_cities = ref(cities);
    const list_provinces = ref(provinces);

    return {
      right: ref(false),
      list_cities,
      list_provinces,
      cities,

      filterFn(val: string, update: (arg0: { (): void; (): void }) => void) {
        if (val === '') {
          update(() => {
            list_cities.value = cities;
          });
          return;
        }

        update(() => {
          const needle = val.toLowerCase();
          list_cities.value = cities.filter(
            (v: string) => v.toLowerCase().indexOf(needle) > -1,
          );
        });
      },
    };
  },
});
</script>
