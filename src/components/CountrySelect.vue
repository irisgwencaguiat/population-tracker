<template>
 <select @change="onChange" v-model="selected" class="container w-80 form-select mt-1 block w-full border p-3 rounded">
   <option value=0>Select Country</option>
   <option v-for="country in countries" :value="country.iso3">{{country.country}}</option>
 </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
  data () {
    return {
      selected: 0
    }
  },
  methods: {
    async onChange () {
      this.$emit('get-country-iso3', this.selected)
    }
  }
}
</script>