<template>
  <div
    :class="[
      setShape,
      showData ? 'border-gray-700 scale-125' : 'border-gray-800 scale-0',
    ]"
    class="relative bg-gray-800 rounded-lg cursor-pointer overflow-hidden border-4 transition-all duration-300 ease-in-out"
    @mouseenter="setVisibility"
    @mouseleave="setVisibility"
  >
    <img :src="setContent" alt="" class="w-full h-full" />
    <div
      :class="[showData ? 'opacity-100' : 'opacity-0']"
      class="absolute bottom-0 left-0 w-full bg-gray-800 text-gray-500 text-left p-2 transition-opacity duration-300 ease-in-out"
    >
      <p>Nombre: {{ setName }}</p>
      <p>Alto: {{ setHeight }}</p>
      <p>Ancho: {{ setWitdth }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SampleCard',
  props: {
    rawData: {
      type: Object,
      default: () => ({}),
      required: true,
    },
  },
  data: () => {
    return {
      showData: false,
    }
  },
  computed: {
    setRawData() {
      return this.rawData
    },
    setName() {
      return this.rawData.name
    },
    setContent() {
      return this.rawData.url
    },
    setHeight() {
      return this.rawData.height
    },
    setWitdth() {
      return this.rawData.width
    },
    setShape() {
      let shape = ''

      if (this.setHeight === this.setWitdth) {
        shape = 'row-span-1 col-span-1'
      } else if (this.setHeight > this.setWitdth) {
        shape = 'row-span-2 col-span-1'
      }
      return shape
    },
  },
  methods: {
    setVisibility() {
      this.showData = !this.showData
    },
  },
}
</script>

<style></style>
