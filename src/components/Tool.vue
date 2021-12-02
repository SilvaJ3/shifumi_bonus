<template>
  <div :id="data.name" class="rounded-full w-24 h-24 p-3 bg-white paper shadow-inner flex justify-center items-center cursor-pointer" @click="select(data.name)">
    <img :src="data.image" :alt="'icon-' + data.name" class="w-16 h-16 pointer-events-none">
  </div>
</template>

<script>
export default {
  props: {
    data: Object
  },
  methods: {
    select(value){
      this.$emit("selection", value)
    }
  }
}
</script>

<style>

</style>