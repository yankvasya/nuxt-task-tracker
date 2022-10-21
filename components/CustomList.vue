<template>
  <li
    class="list"
    @drop="onDrop($event, list.id)"
    @dragover.prevent
    @dragenter.prevent
  >
    <h2 class="list__title">{{ list.name }}</h2>

    <ul class="list__tasks tasks">
      <CustomItem
        v-for="task of tasks"
        :key="task.id"
        :item="task"
        class="tasks__task"
        @update:drag="startDrag"
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
  emits: ['update:task-list'],
  methods: {
    startDrag(event, item) {
      event.dataTransfer.dropEffect = 'move'
      event.dataTransfer.effectAllowed = 'move'
      event.dataTransfer.setData('itemID', item.id)
    },
    onDrop(event, list) {
      this.$emit('update:task-list', event, list)
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
