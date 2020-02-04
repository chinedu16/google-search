<template>
  <div class="home">

		<div v-if="noResults">
			Sorry, but no results were found. I blame Apple.
		</div>

		<div v-if="searching">
			<i>Searching...</i>
		</div>

		<div v-if="!searching">
			<i>Done....</i>
		</div>

		<div v-for="result in results" class="result" :key="result.id">
			<img :src="result.artworkUrl100">
			<b>Artist:</b> {{result.artistName}}<br/>
			<b>Track:</b> {{result.trackName}}<br/>
			<b>Released:</b> {{result.releaseDate }}
			<br clear="left">
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
			this.$route.push({name: 'search'})
		} else {
			this.term = this.$route.params.term;
			this.search()
		}
	}
}
</script>




<style scoped>