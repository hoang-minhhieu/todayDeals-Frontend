<!-- Notice lang="scss" -->
<style lang="scss">
.header {
  display: flex;
  justify-content: center;
  background-color: black;
  height: 60px;
}

.navbarBtn {
  margin: 10px;
  font-size: 0.9em;
}

.searchBar {
  margin: 10px;
}

.q-tabs .q-tab__label {
  font-size: 0.9em;
}
</style>

<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="bg-primary text-white">
      <div class="header">
        <q-tabs no-caps>
          <q-tab name="images" label="Khuyến mãi" />
          <q-tab name="videos" label="Mã giảm giá" />
          <q-tab name="articles" label="Miễn phí" />
        </q-tabs>

        <q-input
          v-model="search"
          debounce="500"
          outlined
          color="navy"
          bg-color="white"
          rounded
          placeholder="Tìm kiếm"
          :class="'searchBar'"
          dense
        >
          <template v-slot:prepend>
            <q-icon name="search" color="gray" />
          </template>
          <template v-slot:append>
            <q-icon
              name="close"
              @click="search = ''"
              class="cursor-pointer"
              color="gray"
            />
          </template>
        </q-input>

        <q-btn-dropdown
          no-caps
          :class="'navbarBtn'"
          label="Ngôn ngữ"
          icon="language"
        >
          <q-list>
            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Tiếng Việt</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>English</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>

        <q-btn no-caps :class="'navbarBtn'" color="primary">
          <q-icon name="person" />
          <div>Đăng nhập</div>
        </q-btn>
      </div>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg" />
          </q-avatar>
          <div>Title</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {},

  setup() {
    return {
      search: ref(''),
      onItemClick() {
        // console.log('Clicked on an Item')
      },
    };
  },
});
</script>
