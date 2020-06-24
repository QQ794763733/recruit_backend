<template>
	<div class="admin-edit-box">
		<el-form :model="admin" class="admin-edit-form">
			<el-upload :on-success="uploadSuccess"  :show-file-list="false" name="picture" accept="image/png,image/jpeg"
			 class="avatar-uploader" action="http://localhost:8888/upload/picture">
				<img v-if="admin.picture" :src="admin.picture" class="avatar">
				<i v-else class="el-icon-plus avatar-uploader-icon"></i>
			</el-upload>
			<el-form-item label="账户">
				<el-input :disabled="true" v-model="admin.name"></el-input>
			</el-form-item>
			<el-form-item label="简介">
				<el-input type="textarea" v-model="admin.introduce"></el-input>
			</el-form-item>
			<el-button>更新资料</el-button>
			<el-button type="warning">修改密码</el-button>
		</el-form>
	</div>
</template>

<script>
	export default {
		name: "EditAdmin",
		data() {
			return {
				admin: {
					name: "",
					picture: "",
					introduce: ""
				}
			}
		},
		mounted() {
			this.admin.name = localStorage.getItem("admin-name");
			this.admin.picture = localStorage.getItem("admin-picture");
			this.admin.introduce = localStorage.getItem("admin-introduce");
		},
		methods: {
			uploadSuccess(response, file, fileList) {
				this.admin.picture = this.$server_host + "/" + response.data;
			}
		}
	}
</script>

<style scoped="scoped">
	.admin-edit-box {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.admin-edit-form {
		width: 500px;
		text-align: center;
	}

	.avatar-uploader .el-upload {
		border: 1px dashed #d9d9d9;
		border-radius: 6px;
		cursor: pointer;
		position: relative;
		overflow: hidden;
	}

	.avatar-uploader .el-upload:hover {
		border-color: #409EFF;
	}

	.avatar-uploader-icon {
		font-size: 28px;
		color: #8c939d;
		width: 178px;
		height: 178px;
		line-height: 178px;
		text-align: center;
	}

	.avatar {
		width: 178px;
		height: 178px;
		display: block;
	}
</style>
