<template>
<div class="navbar">
  <a href="#home">Home</a>
  <a href="#news">News</a>
  <div class="dropdown">
  <button class="dropbtn" v-on:click="showContent">Number of rows
    <i class="fa fa-caret-down"></i>
  </button>
  <div class="dropdown-content" id="myDropdown" v-show="showvar">
    <a href="#">5</a>
    <a href="#">10</a>
    <a href="#">15</a>
    <a href="#">20</a>
    <a href="#">25</a>

  </div>
  </div> 
</div>

</template>

<script>


export default {
  data(){
    return {
      showvar: false,

    }
  },
  methods: {
    showContent: function (){
      let showvar = this.showvar
      showvar = !showvar
      this.showvar = showvar

    }
  }
}
</script>

<style scoped>
.navbar {
  overflow: hidden;
  background-color: #333;
  font-family: Arial, Helvetica, sans-serif;
}

.navbar a {
  float: left;
  font-size: 16px;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

.dropdown {
  float: left;
  overflow: hidden;
}

.dropdown .dropbtn {
  cursor: pointer;
  font-size: 16px;  
  border: none;
  outline: none;
  color: white;
  padding: 14px 16px;
  background-color: inherit;
  font-family: inherit;
  margin: 0;
}

.navbar a:hover, .dropdown:hover .dropbtn, .dropbtn:focus {
  background-color: red;
}

.dropdown-content {
  
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

.dropdown-content a {
  float: none;
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  text-align: left;
}

.dropdown-content a:hover {
  background-color: #ddd;
}

.show {
  display: block;
}
</style>
