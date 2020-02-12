<template>
	<div id="gallery">		
		<div v-for='item in image'>
			<!-- <autor-name></autor-name> -->
			<a :href="item.user.links.html" target="_blank">
				<div id="autor"> <!-- фотка профиля тоже из JSON -->
					<img v-lazy="item.user.profile_image.small" class="jason">
					<div class="text">
						<p>{{item.user.first_name}}
							<br>
						<span>{{"@" + item.user.username}}</span>
						</p>
					</div>			
				</div>
			</a>
	        <img v-lazy="item.urls.regular" class="photo" alt="">
	        <div class="views text-right">
				<span>{{item.likes}}</span>
				<img src="/assets/app/build/galleryUnsplash/likes.png" alt="like icons">
			</div>
	    </div>
		<footer>
			<div class="text-center">
				<div class="d-inline-flex">
					<p @click='prevPage' v-if="page>1">назад</p>
					<p @click='nextPage'>вперед</p>
				</div>				
			</div>
		</footer>
	</div>
</template>

<script>

import JQuery from 'jquery'
  let $ = JQuery

import axios from 'axios'

	export default{
		data(){
			return {
		      image:[],
		      pages:[],
		      url:'https://api.unsplash.com/photos/?client_id=d191c992567636d51760ad629afcfcfc771123ef019e3a7660985c5a2cc3a138',
		      page:1
		    }
		},
		mounted(){
		    this.update(),
		    this.update2()
		  },
		  methods:{
		  	nextPage(){
		  		this.page++
		  		this.update(this.page)
		  		if(this.page > 34){
		  			this.page = 34
		  		}		
      		},
      		prevPage(){
      			this.page--
      			this.update(this.page)
      			if(this.page<1){
      				this.page = 1
      			}
      		},
		  	update(){
		        axios.get(this.url+'&page='+ this.page).then((response)=>{   
		          this.image = response.data
		          console.log(response)

		          console.log(this.image)
		          this.pages = response.headers
		          var pagination = (this.pages)
		          console.log(pagination)
		        })        
      		},     		
		  },
		  components:{
		  	
		  }
	}
</script>
<style>
	.views{
		margin:10px;
	}
	.photo{
		width:100%;
		display:block;
		margin:auto;
	}
	@media (min-width: 320px) and (max-width: 480px){
		
	}
	@media (min-width: 480px) and (max-width: 768px){
		
	}
	@media (min-width: 768px) and (max-width: 1000px){
		
		#gallery{
			padding: 0 54px 0 50px;
			display: grid;
    		grid-template-columns: repeat(2,1fr);
    		grid-gap:1em;
		}
	}
	@media (min-width: 1000px){
		#gallery{
			padding: 0 170px 0 170px;
			display: grid;
    		grid-template-columns: repeat(2,1fr);
    		grid-gap:1em;
		}
	}
#autor{
	width: 160px;
	margin: 10px;
}
	.jason{
		margin-right:10px;
		float:left;		
		width:30px;
		height:30px;
	}
	.text{
		display:table;
		width: 120px;
		height: 27px;
	}
	#autor p{
	font-family: Roboto Condensed;
	font-style: normal;
	font-weight: bold;
	font-size: 12px;
	line-height: 14px;
	color: #333333;
	display:inline-block;
	}
	 span{
		font-family: Roboto Condensed;
		font-style: normal;
		font-weight: normal;
		font-size: 12px;
		line-height: 14px;
		color: #8D8D8D;
	}
	@media (min-width: 320px) and (max-width: 480px){
		margin:10px;
	}
	@media (min-width: 480px) and (max-width: 768px){
		#autor{
			margin: 10px 0 0 20px;
		}	    
	}
	footer{
		position:fixed;
		left:0;
		bottom:0;
		width:100%;
		height: 60px;
		background: #000000;
		opacity: 0.9;
	}
	footer p {
		font-family: Roboto Condensed;
		font-style: normal;
		font-weight: normal;
		font-size: 14px;
		line-height: 60px;
		text-align: center;
		color: #FFFFFF;
		margin:0 5px;
		cursor:pointer;
	}
</style>