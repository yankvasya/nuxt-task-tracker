<template>
  <div class="wrapper">
    <h1 class="wrapper__title">Nuxt task tracker</h1>

    <ul class="wrapper__list">
      <CustomList
        v-for="list of lists"
        :key="list.key"
        :list="list"
        :tasks="currentTasks(list)"
        @update:task-list="updateTaskList"
      />
    </ul>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      lists: [
        { id: 1, name: 'Task' },
        { id: 2, name: 'In progress' },
        { id: 3, name: 'Done!' },
      ],
      tasks: [
        {
          id: 1,
          name: 'Task 1',
          status: 1,
        },
        {
          id: 2,
          name: 'Task 2',
          status: 1,
        },
        {
          id: 3,
          name: 'Task 3',
          status: 2,
        },
        {
          id: 4,
          name: 'Task 4',
          status: 3,
        },
      ],
    }
  },
  computed: {
    currentTasks: (data) => (list) => {
      return data.tasks.filter((task) => task.status === list.id)
    },
  },
  methods: {
    updateTaskList(event, list) {
      const itemID = event.dataTransfer.getData('itemID')
      const item = this.tasks.find((task) => task.id === itemID * 1)
      this.changeTaskStatus(item.id, list)
    },
    changeTaskStatus(id, status) {
      const task = this.tasks.find((task) => task.id === id)
      task.status = status
    },
  },
}
</script>

<style scoped lang="scss">
.wrapper {
  height: 100vh;
  border: 1px solid black;

  &__title {
    text-align: center;
  }

  &__list {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    gap: 10px;
    border: 1px solid black;
    padding: 10px;
    height: 90%;
  }
}
</style>
