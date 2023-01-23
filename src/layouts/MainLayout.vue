<!-- Notice lang="scss" -->
<style lang="scss">
.q-header {
  display: flex;
  justify-content: center;
  background-color: black;
}

.accountBtn {
  margin: 10px;
}

.searchBar {
  background-color: white;
  margin: 10px;
}
</style>

<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-tabs v-model="tab">
        <q-tab name="images" label="Khuyến mãi" />
        <q-tab name="videos" label="Mã giảm giá" />
        <q-tab name="articles" label="Miễn phí" />
      </q-tabs>

      <q-input
        standout
        v-model="text"
        placeholder="Tìm kiếm"
        :class="'searchBar'"
      >
        <template v-slot:prepend>
          <q-icon name="search" color="gray" />
        </template>
        <template v-slot:append>
          <q-icon
            name="close"
            @click="text = ''"
            class="cursor-pointer"
            color="gray"
          />
        </template>
      </q-input>

      <q-btn :class="'accountBtn'" color="grey">
        <q-icon name="person" />
        <div>Đăng nhập</div>
      </q-btn>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {},

  setup() {
    return {
      tab: ref('images'),
      text: ref(''),
    };
  },
});
</script>
