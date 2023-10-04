<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
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
        
      <div class = "q-px-lg q-py-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todaysDate }}</div>
      </div>
      <q-img
        src = "src/statics/forest.jpg"
        class = "header-image absolute-top" />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          Essential Links
        </q-item-label>

        <q-item
          to = "/"
          exact
          clickable
          v-ripple>
          <q-item-section avatar>
            <q-icon name = "today" />
          </q-item-section>

          <q-item-section>
            Week View
          </q-item-section>
        </q-item>

        <q-item
          to = "/Extra"
          exact
          clickable
          v-ripple>
          <q-item-section avatar>
            <q-icon name = "list" />
          </q-item-section>

          <q-item-section>
            Assignment View
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <KeepAlive>
        <router-view />
      </KeepAlive>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { date } from 'quasar'

const linksList = [
  {
    //to: "/Extra",
    //title: 'Todo',
    //caption: 'List of Assignments',
    //icon: 'list',
  }
]

export default defineComponent({
  name: 'MainLayout',

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  },
  computed: {
    todaysDate(){
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'MM/DD/YY')
    }
  }
})

</script>

<style lang = "scss">
  .header-image{
    height: 100%;
    z-index: -1;
    opacity: 1;
    filter: grayscale(0%);
  }
  //quasar dev
</style>