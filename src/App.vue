<template>
  <!-- <Modal v-show="showModal" @closeModal="toggleModal" :msg="msgForModal" /> -->
  <Modal v-show="showModal" @closeModal="toggleModal">
    <p>Message from App slot to Modal component</p>
    <template v-slot:links>
      <a href="#">link 1</a>
      <a href="#">link 2</a>
      <a href="#">link 3</a>
    </template>
  </Modal>
  <p>{{ title }}</p>
  <button @click="toggleModal">Open Modal</button>
</template>

<script>
import Modal from "./components/Modal";

export default {
  name: "App",
  components: {
    Modal,
  },
  data() {
    return {
      title: "App title - p",
      msgForModal: "Message from App data to Modal component",
      showModal: false
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    }
  }
};
</script>

<style lang="sass">
body
  margin: 0
</style>
