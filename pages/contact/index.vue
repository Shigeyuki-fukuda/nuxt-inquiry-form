<template>
  <ContactForm></ContactForm>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import ContactForm from '@/components/contact/Form.vue'

export default defineComponent({
  components: {
    ContactForm
  }
})
</script>
