<template>
  <input
    :type="type"
    :placeholder="placeholder"
    class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
    @input="handleInput"
  />
</template>

<script lang="ts">
import { defineComponent, SetupContext } from '@vue/composition-api'

export default defineComponent({
  name: 'EmailInput',
  props: {
    typs: { type: String, required: true },
    placeholder: { type: String, required: false, default: 'nuxt@example.com' },
  },
  setup(_, context: SetupContext) {
    const handleInput = (e: Event) => {
      const target = e.target as HTMLInputElement
      context.emit('input', target.value)
    }
    return {
      handleInput,
    }
  },
})
</script>
