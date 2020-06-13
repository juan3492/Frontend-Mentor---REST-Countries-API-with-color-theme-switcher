<template>
  <div id="app" :class="mode">
    <Header :mode="mode" v-on:toggle="changeMode()"/>
    <div class="app-content">
      <router-view :mode="mode" />
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header";


export default {
  data () {
    return {
      mode: localStorage.getItem('MODE'),
    }
  },
  components: {
    Header
  },
  /*mounted(){
    /// verificar mode
  },*/
  methods: {
    changeMode() {
      if (this.mode === "dark") {
        this.mode = "light"
        localStorage.setItem('MODE', 'light')
      } else {
        this.mode = "dark"
        localStorage.setItem('MODE', 'dark')
      }
    }
  },
};


</script>

<style lang="css">

  :root{
    --Dark-Blue: hsl(209, 23%, 22%); /** Dark Mode elements */
    --Very-Dark-Blue-BG: hsl(207, 26%, 17%); /** Dark Mode BG */
    --Very-Dark-Blue-Txt: hsl(200, 15%, 8%); /** Light Mode Text */
    --Dark-Gray: hsl(0, 0%, 52%); /** Light Mode Input */
    --Very-Light-Gray: hsl(0, 0%, 98%); /** Light Mode BG */
    --White: hsl(0, 0%, 100%); /** Dark Mode Text & Light Mode Elements */
  }



  html, body{
    margin: 0;
    font-family: 'Nunito Sans', sans-serif;
    font-size: 16px;
    background: var(--Very-Light-Gray);
    color: var(--Very-Dark-Blue-Txt);
    height: 100%;
  }

  .dark{
    background: var(--Very-Dark-Blue-BG);
    color: var(--White);
    min-height: 100%;
  }
</style>
