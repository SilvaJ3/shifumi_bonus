<template>
  <div class="w-full">
    <div v-if="showModal" class="backdrop" @click="showModal = false">
    <div class="rounded-md w-96 flex flex-col border border-white bg-white p-4 modal">
      <div class="flex justify-between items-center mb-6">
        <h1 class="text-xl">RULES</h1>
        <img src="../assets/images/icon-close.svg" alt="" class="h-4 cursor-pointer" @click="showModal = false">
      </div>
      <div class="flex justify-center items-center">
        <img src="../assets/images/image-rules-bonus.svg" alt="">
      </div>
    </div>
  </div>

    <!-- Rules -->
    <div class="flex justify-end">
      <div class="rounded-md border border-white px-4 py-1 cursor-pointer" @click="toggleRules()">
        <h1 class="text-white">RULES</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      showModal: false,
    }
  },
  methods: {
    toggleRules() {
      this.showModal = !this.showModal;
    },
  }
}
</script>

<style>
.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.562);
  z-index: 1;
}

.modal {
  position: absolute;
  top: 25%;
  left: 37%;
  z-index: 2;
  height: 450px;
}
</style>