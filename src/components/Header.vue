<template>
    
    <div class="nav" :class="mode">
      <router-link class="router" to="/"><span> Where in the world? </span></router-link>
      <p @click="changeMode">Dark Mode</p>
    </div>
    
</template>

<script>
  export default {
    props:[
      'mode',
    ],
    methods: {
      changeMode() {
        this.$emit('toggle')        
      }
    },
  }
</script>

<style>

  :root{
    --Dark-Blue: hsl(209, 23%, 22%);          /** Dark Mode elements */
    --Very-Dark-Blue-BG: hsl(207, 26%, 17%);  /** Dark Mode BG */
    --Very-Dark-Blue-Txt: hsl(200, 15%, 8%);  /** Light Mode Text */
    --Dark-Gray: hsl(0, 0%, 52%);             /** Light Mode Input */
    --Very-Light-Gray: hsl(0, 0%, 98%);       /** Light Mode BG */
    --White: hsl(0, 0%, 100%);                /** Dark Mode Text & Light Mode Elements */
  }


  .nav{
    background: var(--White);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 75px;
    font-size: 14px;
    box-shadow: .2px 0 5px rgba(0, 0, 0, .2);
  }

  .nav p{
    margin-right: 20px;
    font-weight: 500;
    font-size: .8em;
    cursor: pointer;
  }

  .router{
    font-weight: 800; 
    margin-left: 20px;
    text-decoration: none;
  }

  .router:visited{
    color: var(--Very-Dark-Blue-Txt);
  }

  .dark .nav{
    background: var(--Dark-Blue);
    color: white;
  }

  .dark .router:visited{
    color: var(--White);
  }

  @media screen and (min-width: 1440px) {
    .nav p{
      margin-right: 75px;
      font-size: 1.2em;
    }
    .router{
      margin-left: 75px;
      font-size: 1.7em ;
    }
  }
</style>