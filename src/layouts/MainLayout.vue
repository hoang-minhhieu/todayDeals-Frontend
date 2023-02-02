<template>
  <q-layout view="hHh lpR fFf">
    <q-header>
      <q-toolbar>
        <q-toolbar-title> Scroll Test </q-toolbar-title>
        <div>Quasar v{{ $q.version }}</div>
        <q-space />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page class="full-height" id="page">
        <q-splitter v-model="splitterRatio">
          <template v-slot:before>
            <div name="tab1" :style="heightStyle">
              <p>Tab 1 Content.</p>
              <q-list>
                <q-item v-for="x in 5" :key="x">
                  Tab three content item {{ x }}
                </q-item>
              </q-list>
            </div>
          </template>
          <template v-slot:after>
            <div name="tab1" :style="heightStyle">
              <q-scroll-area class="fit">
                <p>Tab 1 Content.</p>
                <q-list>
                  <q-item v-for="x in 20" :key="x">
                    Tab three content item {{ x }}
                  </q-item>
                </q-list>
              </q-scroll-area>
            </div>
          </template>
        </q-splitter>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  mounted() {
    window.addEventListener('resize', this.setHeight);
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
      heightStyle: '',
      tabLeft: 'tab1',
      tabRight: 'tab3',
      splitterRatio: 50,
    };
  },
};
</script>
