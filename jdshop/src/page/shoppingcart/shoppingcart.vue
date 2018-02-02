<template>
	<div>
		<!--下拉刷新容器-->
		<div id="pullrefresh" class="mui-content mui-scroll-wrapper">
			<div class="mui-scroll">
				<!--数据列表-->
				<ul class="mui-table-view mui-table-view-chevron"></ul>
			</div>
		</div>
	</div>
</template>

<script>
	import mui from 'static/mui/js/mui.js'
	export default {
		data(){
			return{
				count : 5,
			}
		},
		methods:{
			pullupRefresh() {
				setTimeout(() =>{
					mui('#pullrefresh').pullRefresh().endPullupToRefresh((++this.count > 2)); //参数为true代表没有更多数据了。
					var table = document.body.querySelector('.mui-table-view');
					var cells = document.body.querySelectorAll('.mui-table-view-cell');
					var newCount = cells.length>0?5:20;//首次加载20条，满屏
					for (var i = cells.length, len = i + newCount; i < len; i++) {
						var li = document.createElement('li');
						li.className = 'mui-table-view-cell';
						li.innerHTML = '<a class="mui-navigate-right">Item ' + (i + 1) + '</a>';
						table.appendChild(li);
					}
				}, 1500);
			},

			 addData() {
				var table = document.body.querySelector('.mui-table-view');
				var cells = document.body.querySelectorAll('.mui-table-view-cell');
				for(var i = cells.length, len = i + 5; i < len; i++) {
					var li = document.createElement('li');
					li.className = 'mui-table-view-cell';
					li.innerHTML = '<a class="mui-navigate-right">Item ' + (i + 1) + '</a>';
					//下拉刷新，新纪录插到最前面；
					table.insertBefore(li, table.firstChild);
				}
			},
			/**
			 * 下拉刷新具体业务实现
			 */
			pulldownRefresh() {
				setTimeout(()=> {
					this.addData();
					mui('#pullrefresh').pullRefresh().endPulldownToRefresh();
					mui.toast("为你推荐了5篇文章");
				}, 1500);
			},

		},
		mounted(){
			var that = this;
			mui.init({
				pullRefresh: {
					container: '#pullrefresh',
					down: {
						style:'circle',
						callback: that.pulldownRefresh
					},
					up: {
						auto:true,
						contentrefresh: '正在加载...',
						callback: that.pullupRefresh
					}
				}
			});
		}
	}
</script>

<style>
#pullrefresh{
	position: absolute;
	top: 44px;
}
</style>