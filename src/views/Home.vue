<template>
  <div class="home" :class="mode">
    <div class="filter">
      <input type="search" id="" placeholder="Search for a country..." v-model="filterByName">
      <select v-model="filterByRegion" >
        <option selected value="">All Regions</option>
        <option value="Africa">Africa</option>
        <option value="Americas">Americas</option>
        <option value="Asia">Asia</option>
        <option value="Europe">Europe</option>
        <option value="Oceania">Oceania</option>
      </select>
    </div>
    <div class="cards">
      <CountryCard v-for="country in countryData" 
      :key="country.name" 
      :country="country" 
      v-show="filterName(country.name) && filterRegion(country.region)"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CountryCard from "@/components/CountryCard";

export default {
  name: "Home",
  components: {
    CountryCard
  },
  props: [
    'mode'
  ],
  data() {
    return {
      countryData: [],
      filterByName: '',
      filterByRegion: ''
    }
  },
  mounted () {
    axios.get('https://restcountries.eu/rest/v2/all')
      .then(res => this.countryData = res.data)
      .catch(err => console.log(err))
  },
  methods: {
    filterName(countryName) {
      return countryName.toLowerCase().includes(this.filterByName)
    },
    filterRegion(region) {
      return region.includes(this.filterByRegion)
    },
  },
};
</script>

<style lang="css">
    :root{
    --Dark-Blue: hsl(209, 23%, 22%);          /** Dark Mode elements */
    --Very-Dark-Blue-BG: hsl(207, 26%, 17%);  /** Dark Mode BG */
    --Very-Dark-Blue-Txt: hsl(200, 15%, 8%);  /** Light Mode Text */
    --Dark-Gray: hsl(0, 0%, 52%);             /** Light Mode Input */
    --Very-Light-Gray: hsl(0, 0%, 98%);       /** Light Mode BG */
    --White: hsl(0, 0%, 100%);                /** Dark Mode Text & Light Mode Elements */
  }

  .home{
    margin: 25px 15px;
  }
  input{
    display: block;
    width: 100%;
    height: 50px;
    color: var(--Dark-Gray);
    border-radius: 5px;
    border: 0;
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
    padding-left: 30px;
    max-width: 500px;

  }
  select{
    margin: 40px 0 ;
    width: 50%;
    height: 50px;
    color: var(--Very-Dark-Blue-Txt);
    border: 0;
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
    padding-left: 30px;
    border-radius: 5px;
    padding-right: 30px; 
    max-width: 200px;
  }



  .cards{
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .dark select, 
  .dark input {
    background: var(--Dark-Blue);
    color: var(--White);
  }
  @media screen and (min-width: 1440px) {
    .cards{
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr;
    }

    .filter{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      margin: 50px 25px;
    }

    input{
      margin: 0;
      width: 475px;
      height: 55px;
    }
    select{
      margin: 0;
      height: 55px;
    }

    .home{
      margin: 0 50px
    }
  }

  
</style>