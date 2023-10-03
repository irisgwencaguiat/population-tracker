<template>
  <table class="container w-80 text-center text-3xl font-bold table-auto mt-1 border border-collapse p-3 rounded">
    <thead>
    <tr>
      <th class="border border-blue-200">Year</th>
      <th class="border border-blue-200">Value</th>
    </tr>
    </thead>
    <tbody v-for="(population, index) in paginated">
    <tr :class="index % 2 === 1 ? 'bg-blue-200 text-blue-900' : 'bg-blue-100 text-blue-900'">
      <td class="border border-blue-200">{{population.year}}</td>
      <td class="border border-blue-200">{{population.value}}</td>
    </tr>
    </tbody>

  </table>
  <div class="container text-center">
    <button type="button" class="py-2.5 px-2.5 border border-gray-200" @click="prevPage" :disabled="current == 1">
      <i class="fa-solid fa-chevron-left"></i>
    </button>
    <button type="button" class="py-2.5 px-2.5 border border-gray-200"  @click="nextPage" :disabled="lastPage">
      <i class="fa-solid fa-chevron-right"></i>
    </button>
  </div>
</template>

<script>
export default {
  name:'PopulationTable',
  props: ['populations'],
  data () {
    return {
      pageSize: 10,
      current: 1,
    }
  },
  computed: {
    indexStart() {
      return (this.current - 1) * this.pageSize;
    },
    indexEnd() {
      return this.indexStart + this.pageSize;
    },
    paginated() {
      return this.populations.slice(this.indexStart, this.indexEnd);
    },
    lastPage () {
      return Math.ceil(this.populations.length / this.pageSize) === this.current
    }
  },
  methods: {
    async nextPage () {
      this.current = this.current + 1
    },
    async prevPage () {
      this.current = this.current - 1
    }
  }

}
</script>