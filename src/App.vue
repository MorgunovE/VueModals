<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <Modal v-show="modalFirst"  @close="modalFirst = false"  title="First modal">
            <div slot="body">
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Fugiat, odit.</p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well done</button>
            </div>
          </Modal>
  
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
          <Modal v-show="modalSecond.show"  @close="modalSecond.show = false"  title="Modal with form">
            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name</label>
                <input type="text" required v-model="modalSecond.name">
                <label>Email</label>
                <input type="email" required v-model="modalSecond.email">
                <button class="btn btnPrimary" >Submit</button>
              </form>
            </div>
          </Modal>
  
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
          <ModalValidate v-show="modalValidate" @close="modalValidate = false"/>
        </div>
      </section>
    </div>
  </div>
</template>

<script>

import Modal from '@/components/UI/Modal'
import ModalValidate from '@/components/ModalValidate'
export default {
  name: 'App',
  components: {
    ModalValidate,
    Modal
  },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: '',
      },
      modalValidate: false,
    }
  },
  methods: {
    submitSecondForm(){
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      })
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false
    },
  },
  computed: {
  
  },
}
</script>

