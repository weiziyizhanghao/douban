<template>
		<div class="container">
			<div class="canvas" v-show='loading'>
				<div class="spinner"></div>
			</div>
			<h2>{{title}}</h2>
			<div class="row">
				<div class="col-md-2 text-center" v-for="item in list" :key="item.id">
					<router-link :to="{path:'/detail/'+item.id}">
						<img :src="item.images.large">
						<div class="title">{{item.title}}</div>
					</router-link>
				</div>
			</div>
		</div>
</template>
<script>
export default{
	data(){
		return{
			loading:true,
			title:'',
			list:[]
		}
	},
	props: ['movieType'],// 接收父组件传过来的值 --in_theaters=正在上映的电影  --search==搜索电影
	mounted(){
      this.loadMovieList();
    },
	methods:{
		loadMovieList(){
			this.loading=true;
			let params={
				count:18
			},
			movieUrl='/api/movie/'+this.movieType;
			 if (this.movieType == 'search') {
	          params['q'] = this.$route.params.searchKey;
	        }
	        this.$http.post(movieUrl, params).then((res) => {
	          console.log(res.data)
	          this.list = res.data.subjects;
	          this.title = res.data.title;
	          this.loading = false;
	        })
		}
	}
}
</script>
<style>
	img {
    width: 100%;
    height: 230px;
    vertical-align: middle;
  }
  .row > div {
    margin-bottom: 20px;
  }
  .title {
    height: 20px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
</style>