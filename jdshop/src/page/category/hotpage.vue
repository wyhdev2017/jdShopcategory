<template>
	<div>
		dsaf
		<button @click="captureImage()">拍照</button>
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<br />
		<button @click="captureImage()">拍照</button>
	</div>
</template>

<script>
	import mui from 'static/mui/js/mui.js'
	export default {
		data() {
			return {

			}
		},
		methods: {
 captureImage(){
	var cmr = plus.camera.getCamera();
	var res = cmr.supportedImageResolutions[0];
	var fmt = cmr.supportedImageFormats[0];
	console.log("Resolution: "+res+", Format: "+fmt);
	cmr.captureImage( function( path ){
			alert( "Capture image success: " + path );  
		},
		function( error ) {
			alert( "Capture image failed: " + error.message );
		},
		{resolution:res,format:fmt}
	);
}
		},
		mounted() {
			mui.plusReady(function() {
				console.log("s")
				var cmr = plus.camera.getCamera();
				mui.toast( "Camera supperted image resolutions: " + cmr.supportedImageResolutions );
				mui.init({
					swipeBack: true, //启用右滑关闭功能  
				});
			});
		}
	}
</script>

<style>

</style>