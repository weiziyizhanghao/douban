<template>
	<div>
		<movie-list :movie-type="movieType" ref="updateList"></movie-list>
	</div>
</template>
<script>
import movielist from '@/components/movielist.vue'
export default{
	data(){
		return{
			movieType: 'search'// 搜索类型
		}
	},
	watch:{
		// 监听路由
		'$route'(to,from){
			// 防止返回重复调用
			if (to.path.indexOf('/search/') ==0) {
				// 调用子组件方法
				this.$refs.updateList.loadMovieList();
			}
		}
	},
    components: {
      'movie-list': movielist
    }
}
</script>
<style>
	
</style>