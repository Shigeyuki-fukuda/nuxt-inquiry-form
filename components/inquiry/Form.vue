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
              <Error
                v-if="params.name.$dirty && params.name.$anyInvalid"
                :message="params.name.$message"
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
              <Error
                v-if="params.email.$dirty && params.email.$anyInvalid"
                :message="params.email.$message"
              />
            </div>
            <div class="mb-12">
              <Label> 電話番号 </Label>
              <PhoneInput
                v-model="phone"
                :type="'tel'"
                :placeholder="'0312345678'"
              />
              <Error
                v-if="params.phone.$dirty && params.phone.$anyInvalid"
                :message="params.phone.format.$message"
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
              <Error
                v-if="params.message.$dirty && params.message.$anyInvalid"
                :message="params.message.$message"
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
import { useValidation } from 'vue-composable'
import Headline from '@/components/inquiry/Headline.vue'
import Submitted from '@/components/inquiry/Submitted.vue'
import Label from '@/components/inquiry/Label.vue'
import NameInput from '@/components/inquiry/NameInput.vue'
import EmailInput from '@/components/inquiry/EmailInput.vue'
import PhoneInput from '@/components/inquiry/PhoneInput.vue'
import MessageInput from '@/components/inquiry/MessageInput.vue'
import Button from '@/components/inquiry/Button.vue'
import Error from '@/components/inquiry/Error.vue'

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
    Error,
  },
  setup() {
    const { $axios } = useContext()
    const name = ref('')
    const email = ref('')
    const phone = ref('')
    const message = ref('')
    const isSubmited = ref(false)

    const required = (value: string | null | undefined): Boolean => !!value
    const phoneNumberFormat = (value: string): Boolean =>
      value ? !!value.match(/\d{2,3}-\d{1,4}-\d{4}$/) : true
    const params = useValidation({
      name: {
        $value: name,
        required,
        $message: 'お名前を入力してください',
      },
      email: {
        $value: email,
        required,
        $message: 'メールアドレスを入力してください',
      },
      phone: {
        $value: phone,
        format: {
          $validator: phoneNumberFormat,
          $message: '電話番号の形式が不正です',
        },
      },
      message: {
        $value: message,
        required,
        $message: 'お問い合わせ内容を入力してください',
      },
    })

    const onSubmit = async (): Promise<any> => {
      if (!params.$anyInvalid) {
        return await $axios
          .post('/inquiry', {
            inquiry: {
              name,
              email,
              phone,
              message,
            },
          })
          .then(() => {
            isSubmited.value = true
          })
          .catch(() => {})
      } else {
        return await params.$touch()
      }
    }

    return {
      name,
      email,
      phone,
      message,
      isSubmited,
      params,
      onSubmit,
    }
  },
})
</script>
