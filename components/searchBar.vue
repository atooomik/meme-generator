<template>
  <div class="bg-gray-800 text-gray-500">
    <p>Busca por nombre</p>
    <input type="text" aria-label="Busqueda por nombre o termino" />
    <button @click="filterMemes">Buscar</button>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  props: {
    rawData: {
      type: Array,
      default: () => [],
      required: true,
    },
  },
  computed: {
    setRawData() {
      return this.rawData
    },
  },

  methods: {
    filterMemes() {
      const word = 'Spongebob'
      const filterResults = []
      this.setRawData.forEach((element) => {
        if (element.name.includes(word)) {
          filterResults.push(element)
        }
      })
      console.log(filterResults)
      return filterResults
    },
  },
}
</script>

<style></style>
