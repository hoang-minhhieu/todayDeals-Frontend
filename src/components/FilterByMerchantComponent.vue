<template>
  <q-expansion-item expand-separator label="Web mua bán nổi bật">
    <q-card>
      <q-list bordered separator>
        <q-item tag="label" v-ripple v-for="x in visibleMerchants" :key="x">
          <q-checkbox v-model="selectedMerchants[x].selected" />
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
import { merchants } from 'src/constants/constants';
export default defineComponent({
  name: 'FilterByMerchantComponent',
  setup() {
    const listMerchants = ref(merchants);
    const selectedMerchants = reactive(
      listMerchants.value.reduce((acc, merchant) => {
        acc[merchant] = { selected: false };
        return acc;
      }, {}),
    );
    const visibleMerchants = computed(() => listMerchants.value);
    return {
      merchants,
      selectedMerchants,
      visibleMerchants,
    };
  },
});
</script>
