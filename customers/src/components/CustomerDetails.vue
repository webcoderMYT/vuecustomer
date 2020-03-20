<template>
  <div class="details container">
  	<router-link to="/" class="btn btn-default">返回</router-link>
    	<span class="pull-right">
    		<router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
    			编辑
    		</router-link>
    		<button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">删除</button>
    	</span>
    <ul class="list-group">
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-user">
    			姓名：{{customer.name}}
    		</span>
    	</li>
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-phone-alt"> 
    			电话：{{customer.phone}}
    		</span>
    	</li>
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-plus"> 
    			邮箱：{{customer.email}}
    		</span>
    	</li>
    </ul>

    <ul class="list-group">
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-asterisk">
    			学历：{{customer.education}}
    		</span>
    	</li>
    	<li class="list-group-item">
    		<span class="glyphicon glyphicon-map-marker"> 
    			毕业学校：{{customer.college}}
    		</span>
    	</li>

		<li class="list-group-item">
			<span class="glyphicon glyphicon-asterisk"> 
				职业：{{customer.occupation}}
			</span>
		</li>
		<li class="list-group-item">
			<span class="glyphicon glyphicon-file"> 
				个人简历：{{customer.résumé}}
			</span>
		</li>
    </ul>
  </div>
</template>
<script>
	export default{
		name:"CustomerDetails",
		data(){
			return {
				customer:""
			}
		},
		methods:{
			fetchCustomers(id){
				this.$http.get("http://localhost:3000/users/"+id)
				.then(function(response){
					// console.log(response)
					this.customer = response.body
				})
			},
			deleteCustomer(id){
				// console.log(id)
				this.$http.delete("http://localhost:3000/users/"+id)
				.then(function(response){
					this.$router.push({path:"/",query:{alert:"用户删除成功!"}})
				})
			}
		},
		created(){
			this.fetchCustomers(this.$route.params.id);
		}
	}
</script>
<style scoped></style>