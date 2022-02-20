<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        bottom-slots
        class="col"
        square
        bg-color="white"
        v-model="newTask"
        filled
        placeholder="Add task"
        @keyup.enter="addTask"
        dense
      >
        <template v-slot:append>
          <q-btn
            round
            dense
            flat
            icon="add"
            @click="addTask"
          />
        </template>
      </q-input>
    </div>
    <q-list
      class="bg-white"
      separator
      bordered
    >
      <q-item
        v-for="(task,index) in tasks"
        :key="task.title"
        @click="task.done = !task.done"
        clickable
        :class="{ 'done gb-blue-1' : task.done }"
        v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" class="no-pointer-events"/>
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side
        >
          <q-btn color="primary"
                 flat
                 icon="delete"
                 round
                 dense
                 @click.stop = "deleteTask(index)"
          />
        </q-item-section>
      </q-item>
    </q-list>
    <div
      v-if="!this.tasks.length"
      class="no-tasks absolute-center">
      <q-icon
        name="check"
        size="100px"
        color="primary"
      />
      <div class="text-h5 text-primary text-center">
        No tasks
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
    };
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Really Delete',
        cancel: true,
        persistent: true,
      }).onOk(() => {
        this.tasks.splice(index, 1);
        this.$q.notify('Task Deleted.');
      });
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false,
      });
    },
  },
};
</script>

<style lang="scss">
  .done{
    .q-item__label{
      text-decoration: line-through;
      color: #bbb;
    }
  }

  .no-tasks{
    opacity: 0.5;
  }
</style>
