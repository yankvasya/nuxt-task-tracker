<template>
  <li class="list">
    <h2 class="list__title">{{ list.name }}</h2>

    <ul class="list__tasks tasks">
      <CustomItem
        v-for="task of tasks"
        :key="task.id"
        :item="task"
        class="tasks__task"
      />
    </ul>
  </li>
</template>

<script>
export default {
  name: 'CustomList',
  props: {
    list: {
      default: () => ({ id: 1, name: 'List' }),
      type: Object,
    },
    tasks: {
      default: () => [],
      type: Array,
    },
  },
}
</script>

<style scoped lang="scss">
.list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  border: 1px solid black;
  padding: 10px 50px;

  &__title {
    text-align: center;
  }

  &__tasks {
    display: flex;
    flex-direction: column;
    gap: 10px;
    border: 1px solid black;
    padding: 10px 10px 80px;
  }
}
</style>
