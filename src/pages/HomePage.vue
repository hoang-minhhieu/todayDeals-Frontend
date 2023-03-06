<style scoped lang="scss">
.q-layout {
  background: $backgroundColor;
}
.header {
  display: flex;
  margin-right: auto;
  margin-left: auto;
  width: 50vw;
  background-color: $headerColor;
  height: 60px;
  padding: 0;
  .q-tabs {
    margin-left: 3px;
    .q-tab__label {
      font-size: 0.9em;
    }
  }
}

.filterTabsBar {
  background-color: $filterTabs;
  padding: 0;
  margin-left: 3px;
  .q-tabs {
    padding: 0;
    margin-right: auto;
    margin-left: auto;
    width: 50vw;
    background-color: $filterTabs;
    color: white;
    .q-tab__label {
      font-size: 0.9em;
    }

    .q-checkbox {
      right: 0;
      position: absolute;
    }
  }
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

.searchBar {
  width: 300px;
}

.fi {
  margin-right: 10px;
}

.q-page-container {
  width: 50vw;
  margin-left: auto;
  margin-right: auto;
}

.q-item__section {
  display: contents;
}

.q-item__label {
  align-self: center;
}

.center-side {
  background: $backgroundColor;
  width: 75%;
}

.right-side {
  width: 25%;
  height: fit-content;
  margin: 3px 0 0 5px;
}

.right-side-top {
  background: white;
}

.right-side-bot {
  background: white;
  margin-top: 8px;
}

.q-footer {
  background-color: $filterTabs;
}
</style>

<template>
  <q-layout view="hHh lpR fFf">
    <q-header class="bg-black text-white">
      <q-toolbar class="header">
        <q-tabs align="left" no-caps>
          <q-route-tab :label="translations.header.deals" />
          <q-route-tab :label="translations.header.coupons" />
          <q-route-tab :label="translations.header.free" />
          <q-route-tab :label="translations.header.event" />
          <q-route-tab :label="translations.header.discussion" />
        </q-tabs>

        <q-input
          v-model="search"
          debounce="500"
          outlined
          color="navy"
          bg-color="white"
          rounded
          :placeholder="translations.search"
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
            :label="translations.languages"
            icon="language"
          >
            <q-list>
              <q-item clickable v-close-popup @click="switchLanguage('vn')">
                <q-item-section>
                  <span class="fi fi-vn"></span>
                  <q-item-label>Tiếng Việt</q-item-label>
                </q-item-section>
              </q-item>

              <q-item clickable v-close-popup @click="switchLanguage('en')">
                <q-item-section>
                  <span class="fi fi-gb"></span>
                  <q-item-label>English</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>

          <q-btn no-caps :class="'navbarBtn'" color="primary">
            <q-icon name="person" />
            <div>{{ translations.login }}</div>
          </q-btn>
        </div>
      </q-toolbar>

      <q-toolbar class="filterTabsBar">
        <q-tabs align="left" no-caps>
          <q-tab to="/page1" :label="translations.tabs.newest" />
          <q-tab to="/page2" :label="translations.tabs.hot" />
          <q-checkbox
            keep-color
            dark
            left-label
            v-model="right"
            :label="translations.hideExpired"
          />
        </q-tabs>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <HighlightComponent></HighlightComponent>
      <q-page class="full-height" id="page" style="display: flex">
        <div class="center-side">
          <DealsCardComponent></DealsCardComponent>
        </div>
        <div class="right-side">
          <div class="right-side-top">
            <FilterDealsComponent></FilterDealsComponent>
          </div>
          <div class="right-side-bot">
            <TopDiscussionComponent></TopDiscussionComponent>
          </div>
        </div>
      </q-page>
    </q-page-container>

    <q-footer>
      <q-toolbar>
        <q-toolbar-title>
          <div>Footer</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import FilterDealsComponent from '../components/FilterDealsComponent.vue';
import TopDiscussionComponent from '../components/TopDiscussionComponent.vue';
import DealsCardComponent from '../components/DealsCardComponent.vue';
import HighlightComponent from '../components/HighlightComponent.vue';
import { ref } from 'vue';
import '/node_modules/flag-icons/css/flag-icons.min.css';
import constants from '../constants/constants';
import translations from '../locales/translations';

export default {
  name: 'MainLayout',

  components: {
    FilterDealsComponent,
    TopDiscussionComponent,
    DealsCardComponent,
    HighlightComponent,
  },
  data() {
    return {
      translations: translations[constants.getCurrentLanguage()],
      search: '',
      right: ref(false),
    };
  },

  methods: {
    switchLanguage(language) {
      // Set the currentLanguage property in the config.js file to the new language
      constants.setCurrentLanguage(language);
      // Reload the page to see the changes
      this.translations = translations[language];
    },
  },
};
</script>
