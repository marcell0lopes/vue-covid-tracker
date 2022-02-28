<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select block w-full px-3 py-3 text-base text-gray-700 bg-white bg-clip-padding bg-no-repeat border border-solid border-gray-300 rounded transition ease-in-out mb-4 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
    aria-label="Select country"
  >
    <option value="0">Select Country</option>
    <option v-for="country in countries" :key="country.ID" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],

  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);

      this.$emit('get-country', country);
    },
  },
};
</script>
