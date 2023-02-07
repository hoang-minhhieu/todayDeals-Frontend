<style scoped lang="scss">
.header {
  display: flex;
  margin-right: auto;
  margin-left: auto;
  width: 65vw;
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

.right-side-navbar {
  margin-left: auto;
  display: flex;
}

.q-tabs {
  background-color: #f7941d;
  .q-tab__label {
    font-size: 0.9em;
  }
}

.searchBar {
  width: 300px;
}

.fi {
  margin-right: 10px;
}

.q-page-container {
  width: 65vw;
  margin-left: auto;
  margin-right: auto;
}

.q-item__section {
  display: contents;
}

.q-item__label {
  align-self: center;
}

.left-side {
  background: white;
  width: 20%;
  margin: 5px 0;
  height: fit-content;
}

.center-side {
  background: $bgColor;
  width: 60%;
  margin: 5px;
}

.right-side {
  background: white;
  width: 20%;
  margin: 5px 0;
  height: fit-content;
}
</style>

<template>
  <q-layout view="hHh lpR fFf" style="background: #e3e6e6">
    <q-header class="bg-black text-white">
      <div class="header">
        <q-tabs no-caps>
          <q-tab name="images" label="Khuyến mãi" />
          <q-tab name="videos" label="Mã giảm giá" />
          <q-tab name="articles" label="Miễn phí" />
          <q-tab name="events" label="Sự kiện" />
          <q-tab name="forum" label="Diễn đàn" />
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

        <div :class="'right-side-navbar'">
          <q-btn-dropdown
            no-caps
            :class="'navbarBtn'"
            label="Ngôn ngữ"
            icon="language"
          >
            <q-list>
              <q-item clickable v-close-popup @click="onItemClick">
                <q-item-section>
                  <span class="fi fi-vn"></span>
                  <q-item-label>Tiếng Việt</q-item-label>
                </q-item-section>
              </q-item>

              <q-item clickable v-close-popup @click="onItemClick">
                <q-item-section>
                  <span class="fi fi-gb"></span>
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
      </div>
    </q-header>

    <q-page-container>
      <q-page class="full-height" id="page" style="display: flex">
        <div class="left-side">
          <FilterDealsComponent></FilterDealsComponent>
        </div>
        <div class="center-side">
          <div name="tab1" :style="heightStyle">
            <DealsCardComponent></DealsCardComponent>
          </div>
        </div>
        <div class="right-side">
          <HighlightComponent></HighlightComponent>
        </div>
      </q-page>
    </q-page-container>

    <q-footer class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <div>Title</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import FilterDealsComponent from '../components/FilterDealsComponent.vue';
import DealsCardComponent from '../components/DealsCardComponent.vue';
import HighlightComponent from '../components/HighlightComponent.vue';
import '/node_modules/flag-icons/css/flag-icons.min.css';
export default {
  name: 'MainLayout',

  components: { FilterDealsComponent, DealsCardComponent, HighlightComponent },
  mounted() {
    this.setHeight();
  },
  methods: {
    setHeight() {
      const panelTop = document.getElementById('page').offsetTop;
      const panelHeight = window.innerHeight - panelTop - 60;
      this.heightStyle = 'height: ' + panelHeight + 'px';
    },
  },
  data() {
    return {
      search: '',
      heightStyle: '',
    };
  },
};
</script>
