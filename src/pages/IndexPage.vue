<style>
.q-page {
  background-color: #e3e6e6;
}

.subNavBar {
  background-color: white;
}

.right-subNavBar {
  display: flex;
  width: 65vw;
}

.select-subNavBar {
  width: 200px;
  align-self: center;
  margin: 10px 15px 10px 0;
}

.side-panel-area {
  margin-top: 60px;
  text-align: center;
}

.left-panel-area {
  background: red;
  width: 25%;
  height: 501px;
  position: sticky;
  top: 0;
  margin-top: 60px;
}

.main-area {
  display: flex;
  margin-top: 60px;
  width: 50%;
  margin-left: auto;
  margin-right: auto;
}

.right-panel-area {
  background: green;
  width: 25%;
  height: 501px;
  position: sticky;
  top: 0;
  margin-top: 60px;
}

.list-cities div.q-field__native span {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>

<template>
  <q-page class="full-width row justify-center" style="height: 1500px">
    <div style="width: 65vw; display: flex">
      <div class="left-panel-area">
        <CategorieComponent></CategorieComponent>
      </div>
      <div class="main-area">
        <DealsCardComponent> </DealsCardComponent>
      </div>
      <div class="right-panel-area">
        <HighlightComponent></HighlightComponent>
      </div>
    </div>

    <!-- <q-page-sticky expand position="top" :class="'subNavBar'">
      <div :class="'right-subNavBar'">
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
    </q-page-sticky> -->
  </q-page>
</template>

<script lang="ts">
import DealsCardComponent from 'src/components/DealsCardComponent.vue';
import CategorieComponent from 'src/components/CategorieComponent.vue';
import HighlightComponent from 'src/components/HighlightComponent.vue';
import { defineComponent, ref } from 'vue';

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
  name: 'IndexPage',
  components: { CategorieComponent, DealsCardComponent, HighlightComponent },
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
