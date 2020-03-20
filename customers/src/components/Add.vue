<template>
	<div class="Add container">
	<Alert v-if="alert" v-bind:message="alert"></Alert>
		<h1 class="page-header">添加用户</h1>
		<form v-on:submit="addCustomer">
			<div class="well">
				<h4>用户信息</h4>
				<div class="form-group">
					<label>姓名</label>
					<input type="text" class="form-control" placeholder="name" v-model="customer.name">
					<label>手机号码</label>
					<input type="text" class="form-control" placeholder="phone" v-model="customer.phone"><label class="color">{{phone_error}}</label><br>
					<label>邮箱</label>
					<input type="text" class="form-control" placeholder="email" v-model="customer.email"><label class="color">{{email_error}}</label><br>
					<label>学历</label>
					<input type="text" class="form-control" placeholder="education" v-model="customer.education">
					<label>毕业学校</label>
					<input type="text" class="form-control" placeholder="college" v-model="customer.college">
					<label>职业</label>
					<input type="text" class="form-control" placeholder="occupation" v-model="customer.occupation">
					<label>个人简历</label>
					<!-- <input type="text" class="form-control" placeholder="résumé" v-model="customer.résumé"> -->
					<textarea class="form-control" v-model="customer.résumé" rows="10" placeholder="résumé"></textarea><label class="color">{{résumé_error}}</label><br>
				</div>
				<button type="submit" class="btn btn-primary" @click="changetest">添加</button>
			</div>
		</form>
	</div>
</template>
<script>
import Alert from './Alert'
	export default{
		name:"add",
		data(){
			return {
				customer:{},
				phone_error:"",
				email_error:"",
				résumé_error:"",
				alert:""
			}
		},
		methods:{
			addCustomer(event){
				// console.log(123)
				if(!this.customer.name || !this.customer.phone || !this.customer.email || !this.customer.education || !this.customer.college || !this.customer.occupation || !this.customer.résumé){
					// console.log("请填写对应相关信息")
					this.alert = "相关信息不能为空!"
				}else{
					let newCustomer = {
						name:this.customer.name,
						phone:this.customer.phone,
						email:this.customer.email,
						education:this.customer.education,
						college:this.customer.college,
						occupation:this.customer.college,
						résumé:this.customer.résumé
					}
					this.$http.post("http://localhost:3000/users",newCustomer)
					.then(function(response){
						// console.log(response)
						this.$router.push({path:'/',query:{alert:"用户信息添加成功!"}});
					})
					event.preventDefault();
				}
				event.preventDefault();
			},
			changetest(event){
				var phone_reg = /^1[3456789][0-9]{9}$/gi;
				var email_reg = /^[a-zA-Z0-9]+@[a-zA-Z0-9_-]+(\.)+(com)$/gi;
				var résumé_reg = /^[\u4e00-\u9fa5\w\s]{1,20}$/
				if(!phone_reg.test(this.customer.phone)){
					this.phone_error = "请输入正确的电话号码"
					event.preventDefault();
				}else if(!email_reg.test(this.customer.email)){
					this.email_error = "邮箱格式错误，请重新输入"
					event.preventDefault();
				}else if(résumé_reg.test(this.customer.résumé)){
					this.résumé_error = "不少于20个字"
					event.preventDefault();
				}

			}
		},
		components:{
			Alert
		}
	}
</script>
<style scoped>
	label.color{
		color: red
	}
</style>