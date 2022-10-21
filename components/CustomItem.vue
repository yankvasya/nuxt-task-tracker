<template>
  <li
    class="task"
    :class="{ 'task--drag': isDrag }"
    draggable="true"
    @dragstart="startDrag($event)"
    @dragend="endDrag()"
  >
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
  emits: ['update:drag'],
  data() {
    return {
      isDrag: false,
    }
  },
  methods: {
    startDrag(event) {
      this.isDrag = true
      this.$emit('update:drag', event, this.item)
    },
    endDrag() {
      this.isDrag = false
    },
  },
}
</script>

<style lang="scss">
.task {
  cursor: pointer;
  padding: 8px;
  border: 1px solid black;
  border-radius: 5px;

  &--drag {
    transform: scale(1.1);
    background: rgba(128, 128, 128, 0.3);
  }
}
</style>
