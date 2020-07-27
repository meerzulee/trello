<template>
  <div class="task-view">
    <div class="flex flex-col flex-grow items-start justify-between px-4">
      <input
        type="text"
        class="p-2 mr-2 w-full flex-grow text-xl font-bold "
        :value="task.name"
        @change="updateTaskProperty($event, 'name')"
        @keyup.enter="updateTaskProperty($event, 'name')"
      />
      <textarea
        :value="task.description"
        class="relative bg-transparent w-full px-2 mt-2 h-64 border-none leading-normal border"
        @change="updateTaskProperty($event, 'description')"
        @keyup.enter="updateTaskProperty($event, 'name')"
      />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    task() {
      return this.getTask(this.$route.params.id)
    },
    ...mapGetters(['getTask'])
  },
  methods: {
    updateTaskProperty(e, key) {
      this.$store.commit('UPDATE_TASK', {
        task: this.task,
        key,
        value: e.target.value
      })
    }
  }
}
</script>

<style>
.task-view {
  @apply relative flex flex-row bg-white pin px-4  m-32 mx-auto py-4 text-left rounded shadow;
  max-width: 700px;
}
</style>
