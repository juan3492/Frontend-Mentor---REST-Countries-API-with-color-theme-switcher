<template>
    <div class="card" @click="details(country.name)">
      <div class="flag-zone">
        <img class="country-flag" :src="country.flag" alt="">
      </div>
      <div class="info-zone">
        <h3>{{country.name}}</h3>
        <div class="info-country">
          <p><span class="info-label">Pulation: </span>{{country.population}}</p>
          <p><span class="info-label">Region: </span>{{country.region}}</p>
          <p><span class="info-label">Capital: </span>{{country.capital}}</p>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    props: [
      'country' 
    ],
    methods: {
      details(countryName){
        this.$router.push({
          name: 'Detail',
          params: {countryName: countryName}
          })
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

  .card{
    border-radius: 5px;
    width: 250px;
    height: 300px;
    background: var(--White);
    margin: auto;
    margin-bottom: 40px;
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
    overflow: hidden;
  }

  .card img{
    height: 150px;
    width: 100%;
    object-fit: cover;
  }
  .flag-zone{
    width: 100%;
  }
  .info-zone{
    padding:5px 20px;
  }
  .info-country{
    font-size: .9em;
    line-height: 0.4;
  }
  .info-label{
    font-weight: 600;
  }
  .dark .card{
    background: var(--Dark-Blue);
  }

   @media screen and (min-width: 1440px) {
     .card{
       display: block;
       width: 275px;
       height: 350px;
     }
     .card img{
       height: 175px;
     }
     
   }


</style>