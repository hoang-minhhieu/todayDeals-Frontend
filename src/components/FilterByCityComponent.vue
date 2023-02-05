<template>
  <q-expansion-item expand-separator label="Thành phố">
    <q-card>
      <q-list bordered separator>
        <q-input
          type="text"
          color="primary"
          placeholder="Nhập tên thành phố cần tìm..."
          v-model="searchTerm"
          clearable
        />
        <q-item
          class="q-item"
          tag="label"
          v-ripple
          v-for="x in visibleCities"
          :key="x"
        >
          <q-checkbox v-model="selectedCities[x].selected" />
          <q-item-section>
            <q-item-label>{{ x }}</q-item-label>
          </q-item-section>
        </q-item>
        <q-btn
          flat
          style="color: #f7941d"
          no-caps
          :label="!showAll ? 'Xem thêm' : 'Thu gọn'"
          @click="showAll = !showAll"
        />
      </q-list>
    </q-card>
  </q-expansion-item>
</template>

<script>
import { defineComponent, ref, computed } from 'vue';
import { cities } from '../constants/constants';

export default defineComponent({
  name: 'FilterByCityComponent',
  setup() {
    const listCities = ref(cities);
    const showAll = ref(false);
    const selectedCities = ref(
      listCities.value.reduce((acc, city) => {
        acc[city] = { selected: false };
        return acc;
      }, {}),
    );
    const searchTerm = ref('');

    const filteredCities = computed(() => {
      if (!searchTerm.value) return listCities.value;
      return listCities.value.filter(city =>
        city.toLowerCase().includes(searchTerm.value.toLowerCase()),
      );
    });
    const visibleCities = computed(() => {
      return showAll.value
        ? listCities.value
        : filteredCities.value.slice(0, 5);
    });
    return {
      listCities,
      selectedCities,
      visibleCities,
      showAll,
      filteredCities,
      searchTerm,
    };
  },
});
</script>
