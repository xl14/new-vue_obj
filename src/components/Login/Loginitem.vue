<template>
	<div class="loginitem">
		<el-form :model="ruleForm" :rules="rules" ref="ruleForm" >
		  <el-form-item prop="name">
		    <el-input v-model="ruleForm.name" placeholder="用户名" class="ina"></el-input>
		  </el-form-item>
		  <el-form-item prop="password">
		  	<el-input v-model="ruleForm.password" placeholder="密码" ></el-input>
  			</el-form-item>
  			<el-form-item prop="yzm">
		  		<div class="yzm"><el-input v-model="ruleForm.yzm" placeholder="请输入验证码" class="yzma"></el-input><span class="spana" @click="ntyzm()"><img :src="jsyzm"/></span></div>
  			</el-form-item>
  		 	<el-form-item>
			    <el-button type="primary" @click="login()" class="btnlgn">登陆</el-button>
			</el-form-item>
  		</el-form>
  		<span class="tips">温馨提示:<br/>未登录过的新用户，自动注册注册<br/>过的用户可凭账号密码登录</span>
	</div>
</template>

<script>
	import axios from "axios"
	export default{
		name:"Loginitem",
		 data:function(){
	      return {
	        ruleForm: {
	          name:'',
	          password:'',
	          yzm:''
	        },
	        jsyzm:'',
        rules: {
          name: [
            { required: true, message: '请输入用户名', trigger: 'blur' }
          ],
       		password:[
       			{ required: true, message: '请输入密码', trigger: 'blur' }
       		],
       		yzm:[
       			{ required: true, message: '请输入验证码', trigger: 'blur' }
       		],
        }
      }
   } ,
   methods:{
   	login:function(){
   		axios.post("https://elm.cangdu.org/v2/login",
   					{username:this.ruleForm.name,password:this.ruleForm.password,captcha_code:this.ruleForm.yzm}
					)
   			.then(function(rel){
   				console.log(rel)
   			}).catch(function(err){
				console.log(err);
			})
   	},
   	ntyzm:function(){
   			var that=this;
		   	axios.post("https://elm.cangdu.org/v1/captchas")
		   		.then(function(rel){
		   			console.log(rel.data.code);
		   			that.jsyzm=rel.data.code;
		   		}).catch(function(err){
						console.log(err);
					})
   	}
   },
   created:function(){
   	var that=this;
   	axios.post("https://elm.cangdu.org/v1/captchas")
   		.then(function(rel){
   			console.log(rel.data.code);
   			that.jsyzm=rel.data.code;
   		}).catch(function(err){
				console.log(err);
			})
   }
}
</script>

<style>
	.loginitem{
		width:40%;
		height: 400px;
		background-color: white;
		border-radius: 10px;
		text-align: center;
		margin: 0 auto;
	}
	.el-input{
		width: 70%;
	}
	.ina{
		margin:30px 0 10px 0;
	}
	.el-form-item__error{
		left:90px;
	}
	.el-button{
		width: 70%;
	}
	.tips{
		color: red;
		font-size: 12px;
	}
	.yzma{
		width:60%;
	}
	.yzm{
		width: 70%;
		margin: 0 auto;
	}
	.btnlgn{
		margin-top: 30px;
	}
	.spana{
		width: 37%;
		height: 40px;
		display: inline-block;
		vertical-align: middle;
	}
</style>