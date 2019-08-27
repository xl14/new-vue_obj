<template>
	<div class="login">
		<h1>elm后台管理系统</h1>
		<Loginitem></Loginitem>
	</div>
</template>

<script>
	import Loginitem from "./Loginitem"
	export default{
		name:"Login",
		components:{
			Loginitem
		}
	}
</script>

<style>
	.login{
		width: 100%;
		height: 100%;
		background-color: #324057;
		text-align: center;
	}
	.login h1{
		width: 100%;
		height: 70px;
		line-height: 70px;
		color: white;
		font-weight: 10;
		padding-top:150px;
	}
</style>