<template>
	<div class="sn_layout" @mousewheel="scrollToTop">
		<other-header-bar class="ahead" v-show='!headerBarShow'></other-header-bar>
		<header-bar class="ahead" v-show='headerBarShow'></header-bar>
		<router-view class="abody" id="myData" @hasLoad="hasLoad"></router-view>
		<footer-bar class="aft"></footer-bar>
		<loading v-if="!loadingFlag"></loading>
	</div>
</template>

<script>
	import FooterBar from 'components/footbar'
	import Loading from 'components/loading/loading.vue'
	import HeaderBar from 'components/headbar.vue'
	import OtherHeaderBar from 'components/otherHeaderbar.vue'
	import { mapState, mapActions, mapGetters } from 'vuex';
	
	import mui from 'static/mui/js/mui.js'
	export default {
		data() {
			return {
				loadingFlag: false
			}
		},
		components: {
			FooterBar,
			HeaderBar,
			OtherHeaderBar,
			Loading
		},
		methods: {
			...mapActions(['changeTopShow', 'reduceCarNum']),
			scrollToTop(e) {
				let curHeight = document.documentElement.scrollTop || document.body.scrollTop;
				var offsetTop = document.querySelector('.abody').offsetTop
				if(curHeight > offsetTop) {
					this.$store.dispatch('changeTopShow', true)
				} else {
					this.$store.dispatch('changeTopShow', false)
				}
			},
			hasLoad() {
				//console.log("app")
				setTimeout(()=>{
					this.loadingFlag = true;
					console.log("app2")
					},1000)
				
			}
		},
		computed: {
			...mapState(["topShow", "headerBarShow"]),
			...mapGetters(["gettersCount"])

		},
		 created (){
  	var that = this;
  	
  	//初始化等待框
  	mui.plusReady(function(){
  		plus.nativeUI.showWaiting('初始化')	
  	}  		
  	)
  	setTimeout(function(){
  		mui.plusReady(function(){
  			plus.nativeUI.closeWaiting();		
  		}  		
  	)
  		//that.$router.push('/home')
  	},1000)
  	setTimeout(()=>{
					this.loadingFlag = true;
					console.log("app2")
					},1000)
		 	
  }

	}
</script>

<style scoped="scoped" lang="less">
	@import url("./common/less/variables.less");
	.sn_layout {
		width: 100%;
		max-width: 750px;
		min-width: 320px;
		margin: 0 auto;
		padding-top: 90/@bs;
		padding-bottom: 100/@bs;
		.ahead {
			/*width: 100%;
    height: 5rem;
    position: fixed;
    top: 0;
    left: 0;
    z-index:10;*/
		}
		.abody {
			width: 100%;
			/*margin: 0;
			padding: 0;*/
			background-color: #795DA3;
			/*height: 100%;
			min-height: 46rem;*/
			/*background-color: hotpink;*/
			/*//padding: 5rem 0;*/
		}
		.aft {
			width: 100%;
			position: fixed;
			bottom: 0;
			left: 0;
			z-index: 10;
		}
	}
	/*https://m.jd.com/index/recommend.action?_format_=json&page=1*/
</style>