<template>
  <div>
			<form class="form-horizontal" role="form">
				<div class="form-group">
					<label for="firstname" class="col-sm-1 control-label">姓名</label>
					<div class="col-sm-10">
						<input type="text" class="form-control" id="name" v-model="newEmp.name" placeholder="请输入姓名">
					</div>
				</div>
				<div class="form-group">
					<label for="lastname" class="col-sm-1 control-label">年龄</label>
					<div class="col-sm-10">
						<input type="text" class="form-control" id="age" v-model="newEmp.age" placeholder="请输入年龄">
					</div>
				</div>
				<div class="form-group">
					<label for="lastname" class="col-sm-1 control-label">性别</label>
					<div class="col-sm-10">
						<input type="text" class="form-control" id="sex" v-model="newEmp.sex" placeholder="请输入性别">
					</div>
				</div>
				<div class="form-group">
					<div class="col-sm-10 col-sm-offset-1">
						<button type="button" class="btn btn-default" @click="updateEmp()">修改</button>
					</div>
				</div>
			</form>
  </div>
</template>

<script>
export default {
  name: 'EmpAdd',
  data () {
    return {
    	newEmp:{
    		eid:'',
    		name:'',
    		age:'',
    		sex:''
    	}
    }
  },
  created(){
  	this.toUpdate();
  },
  methods:{
  	toUpdate:function(){
  		
  		var eid = this.$route.query.eid;
  		this.$http.get("http://localhost:8081/emp",{
  			params:{
  				eid:eid
  			}
  		}).then(
  			function(result){
  				this.newEmp = result.body[0];
  			},
  			function(error){
  				console.log("加载失败"+error);
  			}
  		)
  	},
  	updateEmp:function(){
  		this.$http.put("http://localhost:8081/emp",{
  			eid:this.newEmp.eid,
  			name:this.newEmp.name,
  			age:this.newEmp.age,
  			sex:this.newEmp.sex
  		}).then(
  			function(result){
  				
  				this.$router.push({
  					path:"/"
  				})
  				/*this.$router.go(-1);*/
  			},
  			function(error){
  				console.log(error);
  			}
  		)
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

