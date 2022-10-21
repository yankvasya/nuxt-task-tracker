<template>
  <li class="task">
    <h4 class="task__title">{{ item.name }}</h4>
  </li>
</template>

<script>
export default {
  name: 'CustomList',
  props: {
    item: {
      type: Object,
      default: () => ({
        id: 1,
        name: 'Task',
      }),
    },
  },
}
</script>

<style lang="scss">
.task {
  padding: 8px;
  border: 1px solid black;
  border-radius: 5px;
}
</style>
