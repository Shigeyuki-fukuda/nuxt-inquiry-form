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
              <NameInput
                v-model="name"
                :type="'text'"
                :placeholder="'お名前太郎'"
              />
            </div>
            <div class="mb-12">
              <Label>
                メールアドレス <span class="text-xs text-red-500">(必須)</span>
              </Label>
              <EmailInput
                v-model="email"
                :type="'email'"
                :placeholder="'your@example.com'"
              />
            </div>
            <div class="mb-12">
              <Label> 電話番号 </Label>
              <PhoneInput
                v-model="phone"
                :type="'tel'"
                :placeholder="'0312345678'"
              />
            </div>
            <div class="mb-12">
              <Label>
                内容 <span class="text-xs text-red-500">(必須)</span>
              </Label>
              <MessageInput
                v-model="message"
                :placeholder="'お問い合わせ内容です'"
              />
            </div>
            <div class="mb-12">
              <Button @click="onSubmit">送信する</Button>
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
import NameInput from '@/components/contact/NameInput.vue'
import EmailInput from '@/components/contact/EmailInput.vue'
import PhoneInput from '@/components/contact/PhoneInput.vue'
import MessageInput from '@/components/contact/MessageInput.vue'
import Button from '@/components/contact/Button.vue'

export default defineComponent({
  name: 'Form',
  components: {
    Headline,
    Submitted,
    Label,
    NameInput,
    EmailInput,
    PhoneInput,
    MessageInput,
    Button,
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
