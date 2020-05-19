<template>
  <div class="about">
	  
	  <el-form :inline="true" :model="findform" class="demo-form-inline">
	    <el-form-item label="姓名">
	      <el-input v-model="findform.name" placeholder="审批人"></el-input>
	    </el-form-item>
	    <el-form-item label="价格">
	      <el-input v-model="findform.price" placeholder="审批人"></el-input>
	    </el-form-item>
	    <el-form-item>
	      <el-button type="primary" @click="findall">查询</el-button>
	    </el-form-item>
	  </el-form>
	  
	  <el-button type="text" @click="dialogVisible = true">添加</el-button>
	  
	  <el-dialog
	    title="提示"
	    :visible.sync="dialogVisible"
	    width="30%">
		
		<el-form :model="formInline" :rules="rules" ref="formInline" label-width="100px" class="demo-ruleForm">
		  <el-form-item label="姓名" prop="name">
		    <el-input v-model="formInline.name" placeholder="审批人"></el-input>
		  </el-form-item>
		  <el-form-item label="图片">
		    <el-upload
			  name="file"
		      class="avatar-uploader"
		      action="http://laptop-bk2s4m4m:8200/api/upload"
		      :show-file-list="false"
		      :on-success="handleAvatarSuccess"
		      :before-upload="beforeAvatarUpload">
		      <img v-if="imageUrl" :src="imageUrl" class="avatar">
		      <i v-else class="el-icon-plus avatar-uploader-icon"></i>
		    </el-upload>
		  </el-form-item>
		  <el-form-item label="原价" prop="price">
		    <el-input v-model="formInline.price" placeholder="审批人"></el-input>
		  </el-form-item>
		  <el-form-item label="买点" prop="piont">
		    <el-input v-model="formInline.piont" placeholder="审批人"></el-input>
		  </el-form-item>
		  <el-form-item label="描述" prop="xnr">
		    <el-input v-model="formInline.xnr" placeholder="审批人"></el-input>
		  </el-form-item>
		  <el-form-item label="秒杀价" prop="killprice">
		    <el-input v-model="formInline.killprice" placeholder="审批人"></el-input>
		  </el-form-item>
		  <el-form-item>
		    <el-button type="primary" @click="onSubmit">添加</el-button>
		  </el-form-item>
		</el-form>
		
	    <span slot="footer" class="dialog-footer">
	      <el-button @click="dialogVisible = false">取 消</el-button>
	      <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
	    </span>
	  </el-dialog>
	  
	  <!-- 修改 -->
	  <el-dialog
	    title="提示"
	    :visible.sync="upddialogVisible"
	    width="30%">
	  		
	  		<el-form :inline="true" :model="updformInline" class="demo-form-inline">
	  		  <el-form-item label="姓名">
	  		    <el-input v-model="updformInline.name" placeholder="审批人"></el-input>
	  		  </el-form-item>
	  		  <el-form-item label="图片">
	  		    <el-upload
	  			  name="file"
	  		      class="avatar-uploader"
	  		      action="http://laptop-bk2s4m4m:8200/api/upload"
	  		      :show-file-list="false"
	  		      :on-success="handleAvatarSuccess"
	  		      :before-upload="beforeAvatarUpload">
	  		      <img v-if="imageUrl" :src="imageUrl" class="avatar">
	  		      <i v-else class="el-icon-plus avatar-uploader-icon"></i>
	  		    </el-upload>
	  		  </el-form-item>
	  		  <el-form-item label="原价">
	  		    <el-input v-model="updformInline.price" placeholder="审批人"></el-input>
	  		  </el-form-item>
	  		  <el-form-item label="买点">
	  		    <el-input v-model="updformInline.piont" placeholder="审批人"></el-input>
	  		  </el-form-item>
	  		  <el-form-item label="描述">
	  		    <el-input v-model="updformInline.xnr" placeholder="审批人"></el-input>
	  		  </el-form-item>
	  		  <el-form-item label="秒杀价">
	  		    <el-input v-model="updformInline.killprice" placeholder="审批人"></el-input>
	  		  </el-form-item>
	  		  <el-form-item>
	  		    <el-button type="primary" @click="upd">修改</el-button>
	  		  </el-form-item>
	  		</el-form>
	  		
	    <span slot="footer" class="dialog-footer">
	      <el-button @click="dialogVisible = false">取 消</el-button>
	      <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
	    </span>
	  </el-dialog>
	  <!-- 修改完 -->
	  
	 <template>
	    <el-table
	      :data="tableData"
	      style="width: 100%">
	      <el-table-column
	        prop="name"
	        label="名称"
	        width="180">
	      </el-table-column>
		  
	      <el-table-column
	        prop="piont"
	        label="买点"
	        width="180">
	      </el-table-column>
		  
	      <el-table-column
	        label="图片">
			<template slot-scope="per">
							 <div class="block" v-for="fit in fits" :key="fit">
							     <span class="demonstration">{{ fit }}</span>
							     <el-image
							       style="width: 100px; height: 100px"
							       :src="per.row.img"
							       :fit="fit"></el-image>
							   </div>
			</template>
	      </el-table-column>
		  
		  <el-table-column
		    prop="price"
			sortable
		    label="原价">
		  </el-table-column>
		  
		  <el-table-column
		    prop="killprice"
		    label="杀价">
		  </el-table-column>
		  
		  <el-table-column
		    prop="xnr"
		    label="描述">
		  </el-table-column>
		  
		  <el-table-column
		    prop="shon.name"
		    label="地址">
		  </el-table-column>
		  
		  <el-table-column
		    prop="yno"
		    label="是否上架">
		  </el-table-column>
		  
		  <el-table-column>
			  <template slot-scope="per">
				  <el-button type="text" @click="upddialogVisi(per.row)">修改</el-button>
				  <el-button type="text" @click="del(per.row)">删除</el-button>
				  <el-button type="text" @click="up(per.row)">上架</el-button>
				  <el-button type="text" @click="out(per.row)">下架</el-button>
		      </template>
		  </el-table-column>
	    </el-table>
		
		<el-pagination
		      @size-change="handleSizeChange"
		      @current-change="handleCurrentChange"
		      :current-page="currentPage"
		      :page-sizes="[100, 200, 300, 400]"
		      :page-size="100"
		      layout="total, sizes, prev, pager, next, jumper"
		      :total="400">
		    </el-pagination>
		
	  </template>
  </div>
</template>

<script>
    export default {
      data() {
        return {
          tableData: [],
		   dialogVisible: false,
		   upddialogVisible:false,
		   formInline: {
		             name: '',
		             img: '',
					 price: '',
					 piont: '',
					 xnr: '',
					 killprice: ''
		           },
				   updformInline:{
					   id:'',
					   name: '',
					   img: '',
					   price: '',
					   piont: '',
					   xnr: '',
					   killprice: ''
				   },
				   findform:{
					   name:'',
					   price:''
				   },
				   imageUrl:'',
				   fits: ['fill'],
				   currentPage:1,
				   rules:{
					   name:[
						   { required: true, message: '请输入活动名称', trigger: 'blur' }
					   ],
					   price:[
					   						   { required: true, message: '请输入活动名称', trigger: 'blur' }
					   ],
					   piont:[
					   						   { required: true, message: '请输入活动名称', trigger: 'blur' }
					   ],
					   xnr:[
					   						   { required: true, message: '请输入活动名称', trigger: 'blur' }
					   ],
					   killprice:[
					   						   { required: true, message: '请输入活动名称', trigger: 'blur' }
					   ]
				   }
        }
      },
	  created() {
	  	this.initData();
	  },
	  methods:{
		  initData(){//查找
			  console.log(this.findform.price)
			  this.axios.get('http://laptop-bk2s4m4m:8200/api/find',{
				  params:{
					  page:this.currentPage-1,
					name:this.findform.name,
					price:this.findform.price
				  }
			  }).then((rew)=>{
				  this.tableData=rew.data.content;
			  })
		  },
		  onSubmit() {//开始
		          this.axios.get('http://laptop-bk2s4m4m:8200/api/add',{
					  params:{
						  name:this.formInline.name,
						  img: this.formInline.img,
						  price: this.formInline.price,
						  piont: this.formInline.piont,
						  xnr:this.formInline.xnr,
						  killprice:this.formInline.killprice
					  }
				  }).then((rew)=>{
					 this.dialogVisible=false;
					 this.initData();
		          })
		        },
				upd(){//修改
					this.axios.get('http://laptop-bk2s4m4m:8200/api/add',{
										  params:{
											  id:this.updformInline.id,
											  name:this.updformInline.name,
											  img: this.updformInline.img,
											  price: this.updformInline.price,
											  piont: this.updformInline.piont,
											  xnr:this.updformInline.xnr,
											  killprice:this.updformInline.killprice
										  }
					}).then((rew)=>{
						 this.initData();
						this.upddialogVisible=false;
					})
				},
				handleAvatarSuccess(res, file) {
					
						if (res.code==1001) {
							if (this.dialogVisible) {
								this.formInline.img=res.data;
							}else if (this.upddialogVisible) {
								this.updformInline.img=res.data;
							}
							this.imageUrl = URL.createObjectURL(file.raw);
						}else{
							alert('失败')
						}
						
				        
						
				      },
				      beforeAvatarUpload(file) {
				//         const isJPG = file.type === 'image/jpeg';
				//         const isLt2M = file.size / 1024 / 1024 < 2;
				
				//         if (!isJPG) {
				//           this.$message.error('上传头像图片只能是 JPG 格式!');
				//         }
				//         if (!isLt2M) {
				//           this.$message.error('上传头像图片大小不能超过 2MB!');
				//         }
				//         return isJPG && isLt2M;
				      },
					  upddialogVisi(row){
						  Object.assign(this.updformInline,row);
						  this.imageUrl =row.img;
						  this.upddialogVisible=true
					  },
					   handleSizeChange(val) {
					          console.log(`每页 ${val} 条`);
					        },
					        handleCurrentChange(val) {
					          console.log(`当前页: ${val}`);
							  this.currentPage=val;
							  this.initData();
					        },
							del(val){
								this.axios.get('http://laptop-bk2s4m4m:8200/api/del',{
												  params:{
													  id:val.id
												  }
								}).then((rew)=>{
									this.initData();
								})
							},
							up(row){
								Object.assign(this.updformInline,row);
								this.imageUrl =row.img;
								this.axios.get('http://laptop-bk2s4m4m:8200/api/add',{
													  params:{
														  id:this.updformInline.id,
														  yno:1,
														  name:this.updformInline.name,
														  img: this.updformInline.img,
														  price: this.updformInline.price,
														  piont: this.updformInline.piont,
														  xnr:this.updformInline.xnr,
														  killprice:this.updformInline.killprice
													  }
								}).then((rew)=>{
									 this.initData();
									this.upddialogVisible=false;
								})
							},
							out(row){
								Object.assign(this.updformInline,row);
								this.imageUrl =row.img;
								this.axios.get('http://laptop-bk2s4m4m:8200/api/add',{
													  params:{
														  id:this.updformInline.id,
														  yno:0,
														  name:this.updformInline.name,
														  img: this.updformInline.img,
														  price: this.updformInline.price,
														  piont: this.updformInline.piont,
														  xnr:this.updformInline.xnr,
														  killprice:this.updformInline.killprice
													  }
								}).then((rew)=>{
									 this.initData();
									this.upddialogVisible=false;
								})
							},
							findall(){
								this.initData();
							}
	  }
    }
  </script>