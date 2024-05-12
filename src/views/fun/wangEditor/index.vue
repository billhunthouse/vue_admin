
<template>
	<div class="layout-pd">
		<el-card shadow="hover" header="AML状态查询审核">

			<el-form
					ref="ruleFormRef"
					style="max-width: 600px"
					:model="ruleForm"
					:rules="rules"
					label-width="auto"
					class="demo-ruleForm"
					:size="formSize"
					status-icon
			>
				<el-form-item label="查询条件" prop="term">
					<el-select v-model="ruleForm.term" placeholder="请选择查询条件">
						<el-option label="Phone Number" value="phone" />
						<el-option label="Customer Id" value="customer_id" />
					</el-select>
				</el-form-item>

				<el-form-item label="值" prop="values">
					<el-input v-model="ruleForm.values" />
				</el-form-item>

				<el-form-item label="状态" prop="term">
					<el-input v-model="Result.values" />
				</el-form-item>

				<el-form-item>
					<el-button type="primary" @click="submitForm(ruleFormRef)">
						Submit
					</el-button>
					<el-button @click="resetForm(ruleFormRef)">Reset</el-button>
				</el-form-item>
			</el-form>

		</el-card>
	</div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'
import axios from 'axios'

interface RuleForm {
	values: string
	term: string
	count: string
	date1: string
	date2: string
	delivery: boolean
	type: string[]
	resource: string
	desc: string
}

const formSize = ref('default')
const ruleFormRef = ref<FormInstance>()
const ruleForm = reactive<RuleForm>({
	values:'',
	term: '',
	count: '',
	date1: '',
	date2: '',
	delivery: false,
	type: [],
	resource: '',
	desc: '',
})


const Result = reactive<RuleForm>({
	values: '',
	term: '',
	count: '',
	date1: '',
	date2: '',
	delivery: false,
	type: [],
	resource: '',
	desc: '',
})
const rules = reactive<FormRules<RuleForm>>({
	values: [
		{ min: 3, max: 80, message: 'Length should be 9 to 80', trigger: 'blur' },
	],
})

//

const submitForm = async (formEl) => {
	if (!formEl) return
	formEl.validate((valid) => {
		if (valid) {
			// 在这里执行表单提交的操作
			console.log('表单提交成功！')
			console.log(ruleForm)
			console.log("根据：" + ruleForm.term + "查询")
			console.log("具体值是：" + ruleForm.values)

			// 发送POST请求
			axios.post('https://www.baidu.com', {
				term: ruleForm.term,
				values: ruleForm.values
			})
					.then(response => {
						console.log('请求成功：', response)
					})
					.catch(error => {
						console.log('请求失败：', error)
					})

		} else {
			console.log('表单验证失败！')
		}
	})
}


const resetForm = (formEl: FormInstance | undefined) => {
	if (!formEl) return
	formEl.resetFields()
}

const options = Array.from({ length: 10000 }).map((_, idx) => ({
	value: `${idx + 1}`,
	label: `${idx + 1}`,
}))
</script>