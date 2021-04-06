<template>
<div id="app" class="col-sm-12">
	
        <div class="offset">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>Country</th>
              <th>Capital</th>
              <th>Population</th>
			  <th>Languages</th>
			  <th>Translations</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="country in displayedPosts" :key="country.alpha2Code" >
              <td>{{country.name}}</td>
              <td>{{country.capital}}</td>
              <td>{{country.population}}</td>
			  <td>
				  <section v-if="expandLang !== country.alpha2Code">
					  <p>
						  {{country.languages[0].name}}
					  </p>
					  <button @click.prevent="showAllLang(country)" v-if="country.languages.length > 1">Show All</button>
					  
				  </section>
				  <ul v-if="expandLang === country.alpha2Code">
					  
					  <li v-for="lang in country.languages" :key="lang.iso639_1">{{lang.name}}</li>
					  <button @click.prevent="hide(country)" v-if="country.languages.length > 1">Hide</button>
				  </ul>
				  
				  
			  </td>
			  <td>
				  <section v-if="expandTranslation !== country.alpha2Code">
					  <p>{{Object.keys(country.translations)[0]}}:{{country.translations[Object.keys(country.translations)[0]]}}
					  </p>
					  <button @click.prevent="showAllTranslation(country)">Expand</button>
				  </section>
				  <ul v-if="expandTranslation === country.alpha2Code">
					  <li v-for="(translation,key) in country.translations" :key="translation">{{key}}:{{translation}}</li>
					  <button @click.prevent="hide(country)">Hide</button>
				  </ul>
			  </td>
			  <!-- <td>
				  <span v-if="opened1.includes(index)">
				  <p v-for="translation in country.translations" :key="translation.id">{{translation}}</p></span>
				  <span v-else>
					  <p v-for="(translation,index) in country.languages" :key="translation.id"><span v-if="index ==0">{{translation}}</span></p>
				  </span>

				 
				  <button @click="toggle1(index)">Show all</button>
			  </td> -->




			  
          </tr>
          </tbody>
        </table>
        <div class="nav-bar">
          <nav aria-label="Page navigation example">
                  <ul class="pagination">
                      <li class="page-item">
                          <button type="button" class="page-link" v-if="page != 1" @click="page--"> Previous </button>
                      </li>
                      <li class="page-item">
                          <button type="button" class="page-link" v-for="pageNumber in pages.slice(page-1, page+5)" @click="page = pageNumber"> {{pageNumber}} </button>
                      </li>
                      <li class="page-item">
                          <button type="button" @click="page++" v-if="page < pages.length" class="page-link"> Next </button>
                      </li>
                  </ul>
              </nav>
            </div>	
        </div>
      </div>
</template>

<script>
import axios from 'axios';

export default {
    data () {
		return {
			numberOfPages: 10,
			page: 1,
			perPage: 9,
			pages: [],
			posts: [],	
			expandLang:null,
			expandTranslation:null,
				
		}
	},
	mounted() {
        axios
            .get('https://restcountries.eu/rest/v2/all')
            .then(response => (
                this.posts = response.data
                ))
            .catch(error =>(
                console.log(error)
                ))},
    
	methods:{

		showAllLang(item){
			console.log(item.alpha2Code);
			this.expandLang = item.alpha2Code;
			this.expandTranslation = null;

		},
		showAllTranslation(item){
			this.expandTranslation = item.alpha2Code;
			this.expandLang = null;
		},
		hide(item){
			this.expandLang = null;
			this.expandTranslation = null;
		},
	// 	toggle(id) {
    // 	const index = this.opened.indexOf(id);
    //   if (index > -1) {
    //   	this.opened.splice(index, 1)
    //   } else {
    //   	this.opened.push(id);
	// 	this.opened1.push(null);
    //   }
    // },
	// 	toggle1(id) {
	// 		const index = this.opened1.indexOf(id);
    //   if (index > -1) {
    //   	this.opened1.splice(index, 1)
    //   } else {
    //   	this.opened1.push(id);
	// 	  this.opened.push(null);
    //   }

	// 	},

		setPages () {
			let numberOfPages = this.numberOfPages
      		for (let index = 1; index <= numberOfPages; index++) {
        		this.pages.push(index);
			}
		},
		paginate (posts) {
			let page = this.page;
			let perPage = this.perPage;
			let from = (page * perPage) - perPage;
			let to = (page * perPage);
			return  posts.slice(from, to);
		  },
	},
	computed: {
		displayedPosts () {
			return this.paginate(this.posts);
		},


	},
	watch: {
		posts () {
			this.setPages();
		}
	},
	// created(){
	// 	this.getPosts();
	// } ,
	// mounted(){
	// 	this.getPosts();
	// }
}
</script>

<style scoped>
table,th,td {
    border: 2px solid black;
}
table {
	width: 100%;
	border-collapse: collapse;
}
th {
	height: 70px;
	background-color: #4CAF50;
  color: white;
}
th,td {
	padding: 15px;
}
tr:hover {background-color: #f5f5f5;}
tr:nth-child(even) {background-color: #f2f2f2;}
button.page-link {
	display: inline-block;
}
button.page-link {
    font-size: 20px;
    color: #29b3ed;
    font-weight: 500;
}
.offset{
  /* width: 500px !important; */
  margin: 20px auto;  
}
ul{
	display: flex;
	justify-content: center;
	list-style-type:none;
	text-align: center;
	
}
li {
	float: left;
	
}
.collapse{
	float: right;
}
</style>
