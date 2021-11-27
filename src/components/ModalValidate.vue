<template>
  <Modal @close="$emit('close')" title="Modal with form + validate">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <div class="form-item" :class="{ errorInput: $v.name.$error}">
          <label>Name</label>
          <p class="errorText" v-if="!$v.name.required">Field is required!</p>
          <p class="errorText" v-if="!$v.name.minLength">Name must have at least
                                                         {{ $v.name.$params.minLength.min }}!</p>
          <input v-model="name" :class="{ error: $v.name.$error}" @change="$v.name.$touch()">
        </div>
        <div class="form-item" :class="{ errorInput: $v.email.$error}">
          <label>Email</label>
          <p class="errorText" v-if="!$v.email.required">Field is required!</p>
          <p class="errorText" v-if="!$v.email.email">Emil is not correct!</p>
          <input v-model="email" :class="{ error: $v.email.$error}" @change="$v.email.$touch()">
        </div>
        <button class="btn btnPrimary">Submit</button>
      </form>
    </div>
  </Modal>
</template>

<script>
import {required, minLength, email} from 'vuelidate/lib/validators'
// https://vuelidate.js.org/#sub-basic-form
import Modal from '@/components/UI/Modal'

export default {
  name: "ModalValidate",
  components: {Modal},
  data() {
    return {
      name: '',
      email: ''
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    email: {
      required,
      email
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch()
      if(!this.$v.$invalid){
        const user = {
          name: this.name,
          email: this.email,
        }
        console.log(user)
        this.name = ''
        this.email = ''
        this.$v.$reset()
        this.$emit('close')
      }
    }
  },
}
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13px;
  color: red;
}

.form-item {
  &.errorInput .errorText {
    display: block;
  }
}

input.error {
  border-color: red;
}
</style>