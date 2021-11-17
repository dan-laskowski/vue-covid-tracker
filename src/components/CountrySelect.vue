<template>
  <div>Select</div>
  <select name="Countries" id="countries">
    <option v-for="(country, index) in countries" :key="index" :value="item">
      {{ country.Slug }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
};
</script>
