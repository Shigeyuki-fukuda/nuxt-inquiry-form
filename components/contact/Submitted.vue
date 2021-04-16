<template>
  <div class="m-7 text-center">
    <h1>お問い合わせいただきありがとうございます。</h1>
    <h2>ご返信までしばらくお待ちください。</h2>
    <nuxt-link
      to="/"
      type="button"
      class="py-4 px-8 mt-8 text-lg text-gray-50 bg-green-500 hover:bg-green-600 focus:ring-green-600 focus:ring-offset-green-600 transition ease-in duration-200 text-center font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2 rounded-full"
    >
      TOPへ戻る
    </nuxt-link>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'

export default defineComponent({
  name: 'Submitted'
})
</script>
