<template>
  <q-expansion-item expand-separator label="Tỉnh thành">
    <q-card>
      <q-list bordered separator>
        <q-input
          type="text"
          color="primary"
          placeholder="Nhập tên tỉnh thành cần tìm..."
          v-model="searchTerm"
          clearable
        />
        <q-item
          class="q-item"
          tag="label"
          v-ripple
          v-for="x in visibleProvinces"
          :key="x"
        >
          <q-checkbox v-model="selectedProvinces[x].selected" />
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
import { provinces } from '../constants/constants';

export default defineComponent({
  name: 'FilterByProvinceComponent',
  setup() {
    const listProvinces = ref(provinces);
    const showAll = ref(false);
    const selectedProvinces = ref(
      listProvinces.value.reduce((acc, province) => {
        acc[province] = { selected: false };
        return acc;
      }, {}),
    );
    const searchTerm = ref('');

    const filteredProvinces = computed(() => {
      if (!searchTerm.value) return listProvinces.value;
      return listProvinces.value.filter(province =>
        province.toLowerCase().includes(searchTerm.value.toLowerCase()),
      );
    });

    const visibleProvinces = computed(() => {
      return showAll.value
        ? listProvinces.value
        : filteredProvinces.value.slice(0, 5);
    });

    return {
      listProvinces,
      selectedProvinces,
      visibleProvinces,
      showAll,
      filteredProvinces,
      searchTerm,
    };
  },
});
</script>
