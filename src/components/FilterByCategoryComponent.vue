<template>
  <div class="q-pa-md" style="max-width: 350px">
    <q-list bordered class="rounded-borders">
      <q-expansion-item expand-separator label="Xếp loại">
        <q-card>
          <q-list bordered separator>
            <q-item clickable v-ripple>
              <q-item-section>Mới nhất</q-item-section>
            </q-item>

            <q-item clickable v-ripple>
              <q-item-section>Đáng chú ý</q-item-section>
            </q-item>

            <q-item clickable v-ripple>
              <q-item-section>Đang bình luận</q-item-section>
            </q-item>
          </q-list>
        </q-card>
      </q-expansion-item>

      <q-expansion-item expand-separator label="Thành phố">
        <q-card>
          <q-card-section>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quidem,
            eius reprehenderit eos corrupti commodi magni quaerat ex numquam,
            dolorum officiis modi facere maiores architecto suscipit iste
            eveniet doloribus ullam aliquid.
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'FilterByCategoryComponent',
});
</script>
