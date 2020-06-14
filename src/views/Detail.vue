<template>
  <div class="details-container">
    <button class="back" @click="back()">← Back</button>
    <div class="detail-subcont">

    <div class="details-flag">
      <img  :src="country.flag" alt="">
    </div>
      <div class="details">
        <h3 class="details-title">{{ country.name }}</h3>
        <div class="detail-list">
          <ul>
            <li><span class="list-label">Native Name: </span> {{country.nativeName}} </li>
            <li><span class="list-label">Population: </span> {{population}} </li>
            <li><span class="list-label">Region: </span> {{country.region}} </li>
            <li><span class="list-label">Sub Region: </span> {{country.subregion}} </li>
            <li><span class="list-label">Capital: </span> {{country.capital}} </li>
          </ul>
          <ul>
            <li><span class="list-label">Top Level Domain: </span> {{country.topLevelDomain[0]}} </li>
            <li><span class="list-label">Currencies: </span> {{ currencies }} </li>
            <li><span class="list-label">Languages: </span> {{ languages }} </li>
          </ul>
        </div>
        <div class="border">
          <p class="border-countries-title">Border Countries:</p>
          <div class="border-countries-container">
            <button class="border-country" 
            v-for="(coun, index) in borders" 
            :key="index"
            @click="goto(coun.name)"
            > {{coun.name}}</button>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
  import axios from "axios";
  export default {
    data() {
      return {
        country: null,
        borders: []
      }
    },
    mounted () {
      this.getData()
    },
    computed: {
      currencies() {
        var result = [];
        this.country.currencies.forEach(curr => {
          result.push(curr.name)
        });
        return result.join(', ')
      },
      languages(){
        var result = [];
        this.country.languages.forEach(curr => {
          result.push(curr.name)
        });
        return result.join(', ')
      },
      population(){
        return this.country.population.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, '$1,')
      }
    },
    methods: {
      getData(){
        axios.get(`https://restcountries.eu/rest/v2/name/${this.$route.params.countryName}?fullText=true`)
        .then(res=>{
          this.country=res.data[0];
          if(this.country.borders.length > 0){
            var codeList = this.country.borders.join(';')
            axios.get(`https://restcountries.eu/rest/v2/alpha?codes=${codeList}`)
            .then(res=>{this.borders=res.data})
            .catch(err=> console.log("error cargando borders: "+err))
          }
        })
        .catch(err=>{console.log(err)})
      },
      back() {
        this.$router.go(-1)
      },
      goto(countryName) {
        this.$router.replace({
          name: 'Detail',
          params: {countryName: countryName}
        })
        this.getData()
      }
    },
  }
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

  .details-container{
    margin: 30px 20px;
    min-height: 100%;

  }

  .details-flag{
    border: 1px sold red;
    width: 320px;
    height: 250px;
    overflow: hidden;
    margin: auto;
  }

  .details-flag img{
    width: 100%;
    max-height: 250px;
  }

  .back{
    margin-bottom: 50px;
    border: 0;
    border-radius: 5px;
    width: 100px;
    height: 30px;
    background: var(--Very-Light-Gray);
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
    color: var(--Very-Dark-Blue-Txt);

  }

  ul {
    list-style: none;
    text-align: left;
    width: 250px;
    padding: 0;
  }

  li {
    font-size: .8em;
    line-height: 2.3em;
  }

  .list-label{
    font-weight: 600;
  }

  .border-countries-container{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 5px;
    padding-bottom: 50px;
  }

  .border-country{
    border: 0;
    border-radius: 5px;
    width: 100px;
    height: 30px;
    overflow: hidden;
    background: var(--Very-Light-Gray);
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
    color: var(--Very-Dark-Blue-Txt);
  }

  .dark .back, .dark .border-country{
    background: var(--Dark-Blue);
    color: var(--White);
  }

  .border-countries-title{
    font-weight: 600;
  }
  @media screen and (min-width: 1440px) {

    .details-container{
      margin: 75px;
    }

    .detail-subcont{
      display: grid;
      grid-template-columns: 1fr 1fr;

    }

    .details-container{
      height: 100%;
    }

    .detail-list{
      display: flex;
      flex-direction: row;
    }

    .back{
      width: 130px;
      height: 40px;
      font-size: 1em;
    }

    .details-title{
      font-size: 2em;
    }
    .details-flag{

      width: 500px;
      height: 350px;
      margin: 0
    }
    .details-flag img{
      height: 350px;
      max-height: 350px;
    }

    ul{
      margin-top: 0;
      margin-right: 100px;
    }

    li {
      font-size: .9em;
    }

    .border{
      margin-top: 50px;
      display: flex;
      flex-direction: row;
    }
    
    .border-countries-title{
      margin: 0 10px 0 0;
    }

    .border-countries-container{
      grid-template-columns: 1fr 1fr 1fr 1fr;
      grid-gap: 10px;
    }
  }
</style>