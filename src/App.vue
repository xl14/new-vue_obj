<template>
  <div id="app">
    <Login></Login>
    <router-view/>
  </div>
</template>

<script>
	import Login from "@/components/Login/Login"
export default {
	name: 'App',
	components:{
		Login
	},
}
</script>

<style>
html,body,#app {
  width: 100%;
  height: 100%;
}
</style>
