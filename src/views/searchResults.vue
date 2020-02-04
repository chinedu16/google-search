<template>
  <div class="home">

		<div v-if="noResults">
			Sorry, but no results were found. I blame Apple.
		</div>

		<div v-if="searching">
			<i>Searching...</i>
		</div>

		<div class="results">
			<div class="results-body">
				<div v-for="result in results" class="result" :key="result.id">
					<img :src="result.artworkUrl100" width="100%" height="100%">
					<b>Artist:</b> {{result.artistName}}<br/>
					<b>collections</b> {{result.collectionName}}<br/>
					<b>Track:</b> {{result.trackName}}<br/>
					<b>Released:</b> {{result.releaseDate }}
					<br clear="left">
				</div> 
			</div>
			
		</div>	   
  </div>
</template>

<script>
export default {
	name: 'home',
	data () {
		return {
			results:[],
			term: '',
			noResults: false,
			searching: false
		}
	},
	methods: {
		search :function() {
			this.searching = true;
			fetch(`https://itunes.apple.com/search?term=${encodeURIComponent(this.term)}&limit=10&media=music`)
			.then(res => res.json())
			.then(res => {
				this.searching = false;
				this.results = res.results;
				this.noResults = this.results.length === 0;
			});
		}
	},
	created() {
		if (!this.$route.params.term) {
			this.$router.push('/search')
		} else {
			this.term = this.$route.params.term;
			this.search()
		}
	}
}
</script>




<style scoped>
.results {
	display: flex;
}

.results-body {
	margin: auto;
}
</style>