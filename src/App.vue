<template>
  <AppHeader />
  <main class="container" v-if="!loading">
    <div class="grid md:grid-cols-3 gap-4 mb-6 justify-center">
      <CountrySelect
        @get-country="getCountryData"
        :countries="countries"
        class="col-span-2"
      />
      <button
        @click="clearCountryData"
        type="button"
        data-mdb-ripple="true"
        data-mdb-ripple-color="light"
        class="mx-4 w-full inline-block px-6 py-3 bg-emerald-600 text-white font-medium text-sm leading-tight uppercase rounded shadow-md hover:shadow-lg hover:bg-emerald-800 transition duration-150 ease-in-out"
      >
        <i class="fa fa-globe mr-3" /> See Global Stats
      </button>
    </div>
    <hr class="mb-6" />
    <DataTitle :text="title" :dataDate="dataDate" />

    <DataCard :stats="stats" />
  </main>

  <main class="flex flex-col items-center justify-center text-center" v-else>
    <div class="text-gray-500 text-xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" alt="Loading image" class="w-24 m-auto" />
  </main>
</template>

<script>
import AppHeader from '@/components/Header';
import DataTitle from '@/components/DataTitle';
import DataCard from '@/components/DataCard';
import CountrySelect from '@/components/CountrySelect';

export default {
  components: {
    AppHeader,
    DataTitle,
    DataCard,
    CountrySelect,
  },

  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('./assets/hourglass.gif'),
    };
  },

  methods: {
    async fetchCovidData() {
      const data = await fetch('https://api.covid19api.com/summary').then(
        (res) => res.json()
      );
      return data;
    },

    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },

    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = 'Global';
      this.stats = data.Global;
      this.loading = false;
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
