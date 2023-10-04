<template>
  <KeepAlive>
    <q-page class="bg-grey-3 column">
      <q-list class="bg-white" separator bordered>
        <q-item
          v-for="(task, index) in tasks"
          :key="task.title"
          clickable
          @click="task.done = !task.done"
          :class="{ done: task.done }"
          v-ripple
        >
          <q-item-section avatar>
            <q-checkbox v-model="task.done" color="primary" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ task.title }}</q-item-label>
          </q-item-section>
          <q-item-section>
            <q-item-label class="text-right">{{ task.dueDate }}</q-item-label>
          </q-item-section>
          <q-item-section v-if="task.done" side>
            <q-btn
              @click.stop="deleteTask(index)"
              push
              color="primary"
              icon="delete"
              dense
            />
          </q-item-section>
        </q-item>
      </q-list>
      <div class="no-tasks" v-if="!tasks.length">
        <center>
          <q-icon name="check" size="100px" color="primary" />
          <div class="text-h5 text-primary">No Tasks Remaining</div>
        </center>
      </div>
    </q-page>
  </KeepAlive>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      tasks: [
        {
          title: "Research Project",
          dueDate: "11/15/23",
          done: false,
        },
        {
          title: "GEM Pitch",
          dueDate: "10/15/23",
          done: false,
        },
        {
          title: "Poo Banana Pants",
          dueDate: "10/69/23",
          done: false,
        },
      ],
    };
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
});
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #aaa;
  }
}
.no-tasks {
  opacity: 0.8;
}
</style>
