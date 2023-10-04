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
        <q-btn
          flat
          dense
          round
          icon="add"
          aria-label="Add"
          @click="prompt = true"
        />
      </q-toolbar>

      <div class="q-px-lg q-py-xl q-mb-md">
        <div class="text-h2">
          <center>Assignments</center>
        </div>
        <div class="text-subtitle1">
          <center>({{ todaysDate }})</center>
        </div>
      </div>
      <q-img src="src/statics/forest.jpg" class="header-image absolute-top" />
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Essential Links </q-item-label>

        <q-item to="/" exact clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="today" />
          </q-item-section>

          <q-item-section> Week View </q-item-section>
        </q-item>

        <q-item to="/Extra" exact clickable v-ripple>
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>

          <q-item-section> Assignment View </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <KeepAlive>
        <router-view />
      </KeepAlive>
    </q-page-container>
  </q-layout>
  <q-dialog v-model="prompt" persistent>
    <q-card style="min-width: 350px">
      <q-card-section>
        <div class="text-h6">Assignment Name:</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-input
          dense
          v-model="assignment"
          autofocus
          @keyup.enter="prompt = false"
        />
      </q-card-section>
      <q-card-section>
        <div class="text-h6">Due Date:</div>
      </q-card-section>

      <q-card-section class="q-pt-none">
        <q-input
          dense
          v-model="dueDate"
          autofocus
          @keyup.enter="prompt = false"
        />
      </q-card-section>
      <q-card-actions align="right" class="text-primary">
        <q-btn flat label="Cancel" v-close-popup />
        <q-btn flat label="Add Assignment" v-close-popup />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { defineComponent, ref } from "vue";
import { date } from "quasar";

const linksList = [
  {
    //to: "/Extra",
    //title: 'Todo',
    //caption: 'List of Assignments',
    //icon: 'list',
  },
];

export default defineComponent({
  name: "MainLayout",

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      prompt: ref(false),
      assignment: ref(""),
      dueDate: ref(""),
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  computed: {
    todaysDate() {
      let timeStamp = Date.now();
      return date.formatDate(timeStamp, "MM/DD/YY");
    },
  },
  methods: {
    addTask() {
      Extra.tasks.push({
        title: "MainLayout.title",
        dueDate: "MainLayout.dueDate",
        done: false,
      });
    },
  },
});
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 1;
  filter: grayscale(0%);
}
//quasar dev
</style>
