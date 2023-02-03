<style>
.categorie-area {
  position: sticky;
}
</style>

<template>
  <div class="categorie-area">
    <FilterByCategoryComponent></FilterByCategoryComponent>
    <div :class="'select-subNavBar'">
      <q-select
        outlined
        v-model="modelCities"
        multiple
        :options="list_cities"
        dense
      />
    </div>
    <div :class="'select-subNavBar'">
      <q-select
        outlined
        v-model="modelDealsType"
        :options="list_deals_types"
        dense
      ></q-select>
    </div>
    <q-checkbox v-model="right" label="Ẩn hết hạn" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import FilterByCategoryComponent from '../components/FilterByCategoryComponent.vue';

const cities = [
  'Toàn quốc',
  'Hà Nội',
  'TP HCM',
  'Đà Nẵng',
  'Vũng Tàu',
  'Thanh Hóa',
];
const dealsType = ['Mới nhất', 'Được chú ý', 'Đang bình luận'];

export default defineComponent({
  name: 'FilterDealsComponent',

  components: { FilterByCategoryComponent },
  setup() {
    const list_cities = ref(cities);
    const list_deals_types = ref(dealsType);

    return {
      right: ref(false),
      modelCities: ref(['Toàn quốc']),
      modelDealsType: ref('Mới nhất'),
      list_cities,
      list_deals_types,
      cities,
      dealsType,

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
            v => v.toLowerCase().indexOf(needle) > -1,
          );
        });
      },
    };
  },
});
</script>
