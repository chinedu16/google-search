<template>
  <div class="home">
    <head>
			<title>Google Homepage</title>
			<link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">
		</head>

		<body>
		<header>
				<nav>
				<ul id="nav_bar">
						<li class="nav-links" id="gmail"><a href="#">Gmail</a></li>
						<li class="nav-links"><a href="#">Images</a></li>
						<li id="sign_in"><a href="#">Sign In</a></li>
				</ul>  
				</nav>  
		</header>  

		<!-- GOOGLE IMG -->  
		<div class="google">
				<a href="#" id="google_logo"><img src="/src/assets/google-logo.png" alt="googlelogo"/></a>
		</div>

		<!-- FORM SEARCH -->  
		<div class="form">  
				<form>
					<label for="form-search"></label>
					<input v-model="term" type="text" placeholder="Search Google or type URL">
				</form>
		</div>  

		<!-- BUTTONS -->
		<div class= "buttons">  
				<input type="submit" @click="search" value="Google Search" id="google_search">
				<input type="submit" value="I'm Feeling Lucky" id="im_feeling_lucky">
		</div>

		<div v-if="noResults">
			Sorry, but no results were found. I blame Apple.
		</div>

		<div v-if="searching">
			<i>Searching...</i>
		</div>

		<div v-for="result in results" class="result" :key="result.id">
				<img :src="result.artworkUrl100">
				<b>Artist:</b> {{result.artistName}}<br/>
				<b>Track:</b> {{result.trackName}}<br/>
				<b>Released:</b> {{result.releaseDate | formatDate}}
				<br clear="left">
			</div>
		
				
		<!-- FOOTER -->
		<footer>
				<ul class="footer-left">
						<li><a href="#">Advertising</a></li>
						<li><a href="#">Business</a></li>
						<li><a href="#">About</a></li> 
				</ul>
				<ul class="footer-right">    
						<li><a href="#">Privacy</a></li>
						<li><a href="#">Terms</a></li>
						<li><a href="#">Settings</a></li>
				</ul>       
		</footer>      
		</body>
  </div>
</template>

<script>
export default {
	name: 'home',
	data () {
		return {
			term: '',
		}
	},
  components: {

	},

	methods: {
		search: function() {
			this.$router.push({ name: 'search-result', params: { term: this.term } })
		}
	}
}
</script>




<style scoped>
/* BASIC STYLES */
body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
}

header {
  width: 100%;
}

ul {
  list-style: none;
}

/* NAV BAR */
#nav_bar {
  float: right;
}

#nav_bar li {
  display: inline-block;
  padding: 8px;
}

#nav_bar #sign_in {
  background: #4887ef; 
  margin-right: 25px;
  padding: 7px 15px;
  border-radius: 3px; 
  font-weight: bold;
}

.nav-links {
  color: #404040;
}

a {
  text-decoration: none;
  color: inherit;
}

li.nav-links a:hover {
  text-decoration: underline;
}

#sign_in:hover { 
  box-shadow: 1px 1px 5px #999;
}

#sign_in {
  color: #fff;
}

/* GOOGLE AREA */
.google #google_logo {
  text-align: center;
  display: block;
  margin: 0 auto;
  clear: both;
  padding-top: 112px;
  padding-bottom: 20px;
}

.form {
  text-align: center;
}

.form input { 
	background: #fff;
	display: flex;
	border: 1px solid #dfe1e5;
	box-shadow: none;
	border-radius: 24px;
	z-index: 3;
	height: 44px;
	margin: 0 auto;
	width: 482px;
}

.form input:hover {
	box-shadow: 0 1px 6px 0 rgba(32,33,36,0.28);
  border-color: rgba(223,225,229,0);
}

.form input:focus {
	outline: none;
}


.form #form-search {
  padding: 0 8px;
}

/*#form-search:hover {
  border-color: #e4e4e4;
  padding-top: 0;
}*/

.buttons {
  text-align: center;
  padding-top: 18px;
  margin-bottom: 300px;
}

.buttons input {
	background-image: -webkit-linear-gradient(top,#f5f5f5,#f1f1f1);
	background-color: #f2f2f2;
	border: 1px solid #f2f2f2;
	border-radius: 4px;
	color: #5F6368;
	font-family: arial,sans-serif;
	font-size: 14px;
	margin: 11px 4px;
	padding: 0 16px;
	line-height: 27px;
	height: 36px;
	min-width: 54px;
	text-align: center;
	cursor: pointer;
	user-select: none;
}
/* FOOTER */
footer  {
  background: #f2f2f2;
  border-top: solid 2px #e4e4e4;
/*   position: fixed; */
  bottom: 0;
  padding-bottom: 0;
  width: 100%;
  
}

footer ul li {
  display: inline;
  color: #666666;
  font-size: 14px;
  padding: 13px;
}

footer ul {
  float: left;
  padding: 1px;
}

footer ul a:hover {
  text-decoration: underline;
}

.footer-right {
  float: right;
}

/* MEDIA QUERIES */

@media screen and (max-width: 400px) {
 
 li.nav-links a {
    display: none;
  }
  
 #google_logo {
   padding: 0;
 }
  
 .buttons {
   display: none;
 }
  
 #form-search {
   width: 80%;

 }
  
 footer {
   bottom: 0;
 }
  
 footer ul {
   float: none;
   padding-bottom: 2px;
    
 }
  
 .footer-left {
   text-align: center;
   margin: auto; 
   padding-top: 10px;
    
 }
  
 .footer-right {
   float: none;
   text-align: center;
   
 }
}

@media screen and (max-width: 565px) {
 
  li.nav-links a {
    display: none;
  }
  
  
 #google_logo {
   padding: 0;
 }
  
 .buttons {
   display: none;
 }
  
 #form-search {
   width: 80%;

 }
  
 footer {
/*    bottom: 0;
   postion: absolute; */
   position:absolute;
   bottom:0;
   width:100%;
   height:60px;
 }
  
 footer ul {
   float: none;
   padding-bottom: 2px;
    
 }
  
 .footer-left {
   text-align: center;
   margin: auto; 
   padding-top: 10px;
    
 }
  
 .footer-right {
   float: none;
   text-align: center;
   
 }
}

/* <img alt="Google" height="92" id="hplogo" src="/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png" srcset="/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png 1x, /images/branding/googlelogo/2x/googlelogo_color_272x92dp.png 2x" style="padding-top:109px" width="272" onload="typeof google==='object'&amp;&amp;google.aft&amp;&amp;google.aft(this)" data-iml="1580808313509" data-atf="1"> */
</style>