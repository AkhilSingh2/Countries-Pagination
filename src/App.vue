<template>
<div>
  <app-header></app-header>
  <app-table class="main-app"></app-table>
  <app-footer></app-footer>
  
</div>
</template>

<script>
import Header from "./components/Header"
import Footer from "./components/Footer"
import Table from "./components/Table"


export default {
  components: {
    'app-header':Header,
    'app-footer':Footer,
    'app-table' :Table
  }
  
  }

</script>

<style>
body {
  display: grid;
  grid-template-rows: 100px 5rem auto 30%;
}
/* .main-app {
  display: grid;
  align-content: center;
  justify-content: center;
} */

</style>
