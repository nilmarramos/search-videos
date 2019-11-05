<template>
	<div class="container">
		<SearchBar @termChange="onTermChange"/>
		<div class="row">
			<VideoDetail :video="selectedVideo"/>
			<VideoList @videoSelect="onVideoSelect" :videos="videos"/>
		</div>
	</div>
</template>

<script>
	import axios from 'axios'
	import SearchBar from './components/SearchBar'
	import VideoList from './components/VideoList'
	import VideoDetail from './components/VideoDetail'

	const KEY_API = ''

	export default {
		name: "App",
		components: {
			VideoDetail,
			SearchBar,
			VideoList,
		},
		data() {
			return{
				videos: [],
				selectedVideo: null
			}
		},
		methods: {
			onVideoSelect(video) {
				this.selectedVideo = video
			},
			onTermChange(searchTerm) {
				axios.get('https://www.googleapis.com/youtube/v3/search', {
					params: {
						key:KEY_API,
						type: 'video',
						part: 'snippet',
						q: searchTerm
					}
				}).then(resp => {
					this.videos = resp.data.items
				})
			}
		}
	}
</script>

<style scoped>

</style>