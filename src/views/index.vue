<template>
	<div>
		<movie-list :movie-type="movieType"></movie-list>
	</div>
</template>
<script>
import movielist from '@/components/movielist.vue'
export default{
	data(){
		return{
			movieType: 'in_theaters'
		}
	},
	components:{
		'movie-list':movielist
	}
}
</script>
<style>
	
</style>