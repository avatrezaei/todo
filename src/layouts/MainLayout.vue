<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todayDate }}</div>
      </div>
      <q-img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7YKkOSiWEPz73ZA_pJWo5Hk5z4C4_m6WKug&usqp=CAU" class="header-img absolute-top"/>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="250"
      :breakpoint="600"
    >
      <q-scroll-area
        style="height: calc(100% - 150px); margin-top: 192px; border-right: 1px solid #ddd">
        <q-list padding>
          <q-item
            exact
            to="/"
            clickable
            v-ripple>
            <q-item-section avatar>
              <q-icon name="list" />
            </q-item-section>

            <q-item-section>
              Todo
            </q-item-section>
          </q-item>
          <q-item
            clickable
            exact
            to="/help"
            v-ripple>
            <q-item-section avatar>
              <q-icon name="help" />
            </q-item-section>

            <q-item-section>
              Help
            </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>

      <q-img class="absolute-top" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7YKkOSiWEPz73ZA_pJWo5Hk5z4C4_m6WKug&usqp=CAU" style="height: 192px">
        <div class="absolute-bottom bg-transparent">
          <q-avatar size="56px" class="q-mb-sm">
            <img src="https://s.gravatar.com/avatar/f72409a488fae9f36882543af538a787?s=80">
          </q-avatar>
          <div class="text-weight-bold">Avat rezaei</div>
          <div>@avatrezaei</div>
        </div>
      </q-img>
    </q-drawer>

    <q-page-container>
      <keep-alive>
        <router-view />
      </keep-alive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue';
import { date } from 'quasar';

export default defineComponent({
  name: 'MainLayout',

  components: {},
  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  computed: {
    todayDate() {
      const timeStamp = Date.now();
      return date.formatDate(timeStamp, 'dddd D MMM');
    },
  },
});
</script>
<style lang="scss">
  .header-img{
    height: 100%;
    z-index: -1;
    opacity: 0.5;
    filter: grayscale(20%);
}
</style>
