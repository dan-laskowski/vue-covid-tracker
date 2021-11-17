<template>
  <main v-if="!loading"><DataTitle :dataDate="dataDate" :text="title" /></main>
  <main
    class="flex flex-column align-center justify-center text-centers"
    v-else
  >
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching data</div>
    <img class="w-24 m-auto" :src="loadingImage" alt="hourglass" />
  </main>
</template>

<script>
import { DATA_ENDPOINT } from '@/utils/data.js';
import DataTitle from '@/components/DataTitle';

export default {
  name: 'Home',
  components: {
    DataTitle,
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      status: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch(DATA_ENDPOINT);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
