<template>
  <div class="flex items-center min-h-screen bg-black">
    <div class="container mx-auto">
      <div class="max-w-md mx-auto my-10 bg-white p-5 rounded-md shadow-sm">
        <Headline />
        <Submitted v-if="isSubmited" />
        <div v-if="!isSubmited" class="m-7">
          <form>
            <div class="mb-12">
              <Label>
                お名前 <span class="text-xs text-red-500">(必須)</span>
              </Label>
              <input
                v-model="name"
                type="text"
                placeholder="お名前太郎"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-12">
              <Label>
                メールアドレス <span class="text-xs text-red-500">(必須)</span>
              </Label>
              <input
                v-model="email"
                type="email"
                placeholder="your@example.com"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-12">
              <Label> 電話番号 </Label>
              <input
                v-model="phone"
                type="text"
                placeholder="0312345678"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              />
            </div>
            <div class="mb-12">
              <Label>
                内容 <span class="text-xs text-red-500">(必須)</span>
              </Label>
              <textarea
                v-model="message"
                rows="5"
                placeholder="お問い合わせ内容です"
                class="w-full px-3 py-2 placeholder-gray-300 border border-gray-300 rounded-md focus:outline-none focus:ring focus:ring-indigo-100 focus:border-indigo-300 dark:bg-gray-700 dark:text-white dark:placeholder-gray-500 dark:border-gray-600 dark:focus:ring-gray-900 dark:focus:border-gray-500"
              >
              </textarea>
            </div>
            <div class="mb-12">
              <button
                class="w-full px-3 py-4 font-bold text-white bg-green-500 rounded-md focus:bg-green-600 focus:outline-none"
                @click.prevent="onSubmit"
              >
                送信する
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, useContext, ref } from '@nuxtjs/composition-api'
import Headline from '@/components/contact/Headline.vue'
import Submitted from '@/components/contact/Submitted.vue'
import Label from '@/components/contact/Label.vue'

export default defineComponent({
  name: 'Form',
  components: {
    Headline,
    Submitted,
    Label,
  },
  setup() {
    const { $axios } = useContext()
    const name = ref('')
    const email = ref('')
    const phone = ref('')
    const message = ref('')
    const isSubmited = ref(false)

    const onSubmit = async () => {
      return await $axios
        .post('/contact', {
          contact: {
            name,
            email,
            phone,
            message,
          },
        })
        .then(() => (isSubmited.value = true))
        .catch(() => {})
    }

    return {
      name,
      email,
      phone,
      message,
      isSubmited,
      onSubmit,
    }
  },
})
</script>
