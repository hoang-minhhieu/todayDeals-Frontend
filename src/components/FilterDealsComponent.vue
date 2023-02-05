<style scoped>
.q-checkbox {
  margin: 3px 16px;
}

.q-expansion-item {
  background-color: #f6f7fb;
}
</style>
<template>
  <div class="q-pa-md">
    <q-list bordered separator class="rounded-borders">
      <q-checkbox left-label v-model="right" label="Ẩn khuyến mãi hết hạn" />
      <q-separator />
      <FilterByTrendComponent></FilterByTrendComponent>
      <FilterByCategoryComponent></FilterByCategoryComponent>
      <FilterByMerchantComponent></FilterByMerchantComponent>
      <FilterByCityComponent></FilterByCityComponent>
      <FilterByProvinceComponent></FilterByProvinceComponent>
    </q-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import FilterByCategoryComponent from '../components/FilterByCategoryComponent.vue';
import FilterByCityComponent from '../components/FilterByCityComponent.vue';
import FilterByProvinceComponent from './FilterByProvinceComponent.vue';
import FilterByMerchantComponent from './FilterByMerchantComponent.vue';
import FilterByTrendComponent from './FilterByTrendComponent.vue';

export default defineComponent({
  name: 'FilterDealsComponent',

  components: {
    FilterByTrendComponent,
    FilterByCategoryComponent,
    FilterByCityComponent,
    FilterByProvinceComponent,
    FilterByMerchantComponent,
  },
  setup() {
    return {
      right: ref(false),
    };
  },
});
</script>
