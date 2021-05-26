<template>
  <select
      id="country"
      class="form-select mt-10 block w-full border p-3 rounded"
      v-model="selected"
      @change="onChange()"
  >
    <option value="0">Select Country</option>
    <option :value="country" v-for="country in countries">{{country.Country}}</option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelected',
  props: ['countries'],
  data() {
    return {
      selected: 0
    }
  },
  methods: {
    onChange() {
      this.$emit('get-country', this.selected)
    }
  }
}
</script>