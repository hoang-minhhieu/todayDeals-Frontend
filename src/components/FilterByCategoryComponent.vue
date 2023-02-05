<template>
  <q-expansion-item expand-separator label="Danh mục">
    <q-card>
      <q-list bordered separator>
        <q-item tag="label" v-ripple v-for="x in visibleCategories" :key="x">
          <q-checkbox v-model="selectedCategories[x].selected" />
          <q-item-section>
            <q-item-label>{{ x }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-card>
  </q-expansion-item>
</template>

<script>
import { defineComponent, ref, computed, reactive } from 'vue';
import { categories } from 'src/constants/constants';
export default defineComponent({
  name: 'FilterBycategoryComponent',
  setup() {
    const listCategories = ref(categories);
    const selectedCategories = reactive(
      listCategories.value.reduce((acc, category) => {
        acc[category] = { selected: false };
        return acc;
      }, {}),
    );
    const visibleCategories = computed(() => listCategories.value);
    return {
      selectedCategories,
      visibleCategories,
    };
  },
});
</script>
