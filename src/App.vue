<template>
  <HeaderView />
  <main v-if="!loading" class="mb-6 overflow-y-hidden p-4 md:p-6">
    <TitleView :Time="currentDate" :Title="currentTitle" />
    <CasesDeathsView :allInfo="allInfo" />
    <SelectView @haltSelect="updateValue" :Title="currentTitle" :Countries="countries" />
  </main>

  <main v-else>
    <LoadingView />
  </main>

</template>

<script>
  import HeaderView from './components/HeaderView.vue';
  import TitleView from './components/TitleView.vue';
  import CasesDeathsView from './components/CasesDeathsView.vue';
  import SelectView from './components/SelectView.vue';
  import LoadingView from './components/LoadingView.vue';

  export default {
    name: 'App',
    components: {
      HeaderView,
      TitleView,
      CasesDeathsView,
      SelectView,
      LoadingView
    },
    data() {
      return {
        loading: true,
        currentTitle: 'Global',
        currentDate: null,
        countries: [],
        allInfo: {
          newConfirmed: 0,
          totalConfirmed: 0,
          newDeaths: 0,
          totalDeaths: 0
        }
      }
    },
    methods: {
      async fetchData() {
        const res = await fetch("https://api.covid19api.com/summary");
        const data = await res.json();

        return data;
      },
      async updateValue(newTitle) {
        if (newTitle == 0) {
          const data = await this.fetchData();
          this.currentTitle = 'Global';
          this.allInfo.newConfirmed = data.Global.NewConfirmed;
          this.allInfo.totalConfirmed = data.Global.TotalConfirmed;
          this.allInfo.newDeaths = data.Global.NewDeaths;
          this.allInfo.totalDeaths = data.Global.TotalDeaths;
          return;
        }
        this.currentTitle = this.countries[newTitle - 1].Country;
        this.allInfo.newConfirmed = this.countries[newTitle - 1].NewConfirmed;
        this.allInfo.totalConfirmed = this.countries[newTitle - 1].TotalConfirmed;
        this.allInfo.newDeaths = this.countries[newTitle - 1].NewDeaths;
        this.allInfo.totalDeaths = this.countries[newTitle - 1].TotalDeaths;
      }
    },
    async created() {
      const data = await this.fetchData();
      this.loading = false;
      this.currentDate = data.Date;
      this.countries = data.Countries;
      this.allInfo.newConfirmed = data.Global.NewConfirmed;
      this.allInfo.totalConfirmed = data.Global.TotalConfirmed;
      this.allInfo.newDeaths = data.Global.NewDeaths;
      this.allInfo.totalDeaths = data.Global.TotalDeaths;
    }
  }
</script>

<style lang="scss">
  #app {
    text-align: center;
  }
</style>