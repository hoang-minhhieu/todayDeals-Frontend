<template>
  <q-expansion-item expand-separator label="Thịnh hành">
    <q-card>
      <q-list bordered separator>
        <q-item tag="label" v-ripple v-for="x in visibleTrends" :key="x">
          <q-checkbox v-model="selectedTrends[x].selected" />
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
import { trends } from 'src/constants/constants';
export default defineComponent({
  name: 'FilterByTrendComponent',
  setup() {
    const listTrends = ref(trends);
    const selectedTrends = reactive(
      listTrends.value.reduce((acc, trend) => {
        acc[trend] = { selected: false };
        return acc;
      }, {}),
    );
    const visibleTrends = computed(() => listTrends.value);
    return {
      selectedTrends,
      visibleTrends,
    };
  },
});
</script>
