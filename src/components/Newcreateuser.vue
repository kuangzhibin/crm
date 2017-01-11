<template>
	<div class="NewUser">
		
		<el-form ref="form" :model="form" label-width="100px">
			<div class="flx-parent ">
				<div class="flx-childs">
					<el-form-item label="客户姓名" required>
						<el-input v-model="form.name"></el-input>
					</el-form-item>
				</div>      
				<div class="flx-childs">
					<el-form-item label="性别" required>
						<el-radio-group v-model="form.sex">
							<el-radio label="男"></el-radio>
							<el-radio label="女"></el-radio>
						</el-radio-group>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="家长姓名1">
						<el-input v-model="form.parent1"></el-input>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="手机" required>
						<el-input v-model="form.phone"></el-input>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="年级" required>
						<el-select v-model="form.region" placeholder="请选择客户年级">
							<el-option label="区域一" value="shanghai"></el-option>
							<el-option label="区域二" value="beijing"></el-option>
						</el-select>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="信息渠道" required>
						<el-select v-model="form.region" placeholder="信息渠道">
							<el-option label="区域一" value="shanghai"></el-option>
							<el-option label="区域二" value="beijing"></el-option>
						</el-select>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="学校">
						<el-select v-model="form.region" placeholder="学校">
							<el-option label="区域一" value="shanghai"></el-option>
							<el-option label="区域二" value="beijing"></el-option>
						</el-select>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="英文昵称">
						<el-input v-model="form.EnglishName"></el-input>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="身份证">
						<el-input v-model="form.IDcard"></el-input>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="家长姓名2">
						<el-input v-model="form.parent2"></el-input>
					</el-form-item>
				</div>
				<div class="flx-childs">
					<el-form-item label="自定义标签">
						<el-input v-model="form.others"></el-input>
					</el-form-item>
				</div>
				<div class="flx-child">
					<el-form-item label="弱势科目">
						<el-checkbox-group v-model="form.weakSubject">
							<el-checkbox label="语文" name="type"></el-checkbox>
							<el-checkbox label="数学" name="type"></el-checkbox>
							<el-checkbox label="线下主题活动" name="type"></el-checkbox>
							<el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
						</el-checkbox-group>
					</el-form-item>
				</div>
				
			</div>
			
		</el-form>
	</div>
</template>

<script>
	export default {
		name: 'Newcreateuser',
		data() {
			return {
				form: {
		          name: '',
		          region: '',
		          date1: '',
		          date2: '',
		          delivery: false,
		          type: [],
		          resource: '',
		          desc: ''
		        }

			}
		},
	    methods: {
	      onSubmit() {
	        console.log('submit!');
	      }
	    }
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.flx-parent{
	display: flex;
	 flex-flow: row wrap;
}
.flx-childs{
	 flex: 0 0 50%;
}
.flx-child{
	 flex: 0 0 100%;
}
@media (max-width: 768px) {
  .flx-child{
  	flex: 0 0 100%;
  }
}



</style>