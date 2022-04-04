<template>
  <nuxt-link
    class="bg-white flex justify-between rounded-md cursor-pointer group hover:bg-black group overflow-auto"
    :to="{ name: 'tasks-id', params: { id } }"
  >
    <div class="text-xl font-semibold group-hover:text-white pl-4 py-4">
      {{ title }}
    </div>
    <div class="flex gap-x-2 group-hover:gap-x-6">
      <div
        class="font-medium text-lg group-hover:text-white py-4 pr-4 group-hover:pr-0"
      >
        {{ displayStats }}
      </div>
      <div class="justify-around hidden group-hover:w-32 group-hover:flex">
        <div
          class="flex items-center justify-center text-center group-hover:text-white grow hover:bg-blue-400"
          @click.prevent="clickEditHandler"
        >
          Edit
        </div>
        <div
          class="flex items-center justify-center text-center group-hover:text-white grow hover:bg-red-500"
          @click.prevent="clickDeleteHandler"
        >
          Delete
        </div>
      </div>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  props: ['title', 'pomodoroStats', 'index', 'id'],
  methods: {
    clickEditHandler() {
      this.$router.push({ name: 'tasks-id-edit', params: { id: this.id } })
    },
    clickDeleteHandler() {
      this.$emit('taskDeleted', { index: this.index, id: this.id })
    },
  },
  computed: {
    displayStats() {
      return `${this.pomodoroStats.finished}/${this.pomodoroStats.total}`
    },
  },
  emits: ['taskDeleted'],
}
</script>

<style></style>
