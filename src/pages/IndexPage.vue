<style>
.q-page {
  background-color: #e3e6e6;
}

.subNavBar {
  background-color: white;
}

.right-subNavBar {
  display: flex;
  margin-left: auto;
  width: 1200px;
}

.select-subNavBar {
  width: 200px;
  align-self: center;
  margin: 10px 0;
}

.q-checkbox {
  margin-right: 10px;
}

.list-cities div.q-field__native span {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>

<template>
  <q-page class="row items-center justify-evenly">
    <example-component
      title="Example component"
      active
      :todos="todos"
      :meta="meta"
    ></example-component>

    <q-page-sticky expand position="top" :class="'subNavBar'">
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
    </q-page-sticky>
  </q-page>
</template>

<script lang="ts">
import { Todo, Meta } from 'components/models';
import ExampleComponent from 'components/ExampleComponent.vue';
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
  components: { ExampleComponent },
  setup() {
    const list_cities = ref(cities);
    const list_deals_types = ref(dealsType);
    const todos = ref<Todo[]>([
      {
        id: 1,
        content: 'ct1',
      },
      {
        id: 2,
        content: 'ct2',
      },
      {
        id: 3,
        content: 'ct3',
      },
      {
        id: 4,
        content: 'ct4',
      },
      {
        id: 5,
        content: 'ct5',
      },
    ]);
    const meta = ref<Meta>({
      totalCount: 1200,
    });
    return {
      todos,
      meta,
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
