<template>
	<div class="layout-pd">
		<el-card shadow="hover" header="AML状态查询审核">
			
<!--			<el-row :gutter="20">-->
<!--				<el-col :sm="6" class="mb15" v-for="(v, k) in state.topCardItemList" :key="k">-->
<!--					<div class="countup-card-item countup-card-item-box" :style="{ background: `var(${v.color})` }">-->
<!--						<div class="countup-card-item-flex" ref="topCardItemRefs">-->
<!--							<div class="countup-card-item-title pb3">{{ v.title }}</div>-->
<!--							<div class="countup-card-item-title-num pb6"></div>-->
<!--							<div class="countup-card-item-tip pb3">{{ v.tip }}</div>-->
<!--							<div class="countup-card-item-tip-num"></div>-->
<!--						</div>-->
<!--						<i :class="v.icon" :style="{ color: v.iconColor }"></i>-->
<!--					</div>-->
<!--				</el-col>-->
<!--			</el-row>-->
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
				<el-form-item label="查询条件" prop="region">
					<el-select v-model="ruleForm.region" placeholder="请选择查询条件">
						<el-option label="Phone Number" value="phone" />
						<el-option label="Customer Id" value="customer_id" />
					</el-select>
				</el-form-item>

				<el-form-item label="值" prop="name">
					<el-input v-model="ruleForm.name" />
				</el-form-item>
<!--				<el-form-item label="Activity count" prop="count">-->
<!--					<el-select-v2-->
<!--							v-model="ruleForm.count"-->
<!--							placeholder="Activity count"-->
<!--							:options="options"-->
<!--					/>-->
<!--				</el-form-item>-->
<!--				<el-form-item label="Activity time" required>-->
<!--					<el-col :span="11">-->
<!--						<el-form-item prop="date1">-->
<!--							<el-date-picker-->
<!--									v-model="ruleForm.date1"-->
<!--									type="date"-->
<!--									label="Pick a date"-->
<!--									placeholder="Pick a date"-->
<!--									style="width: 100%"-->
<!--							/>-->
<!--						</el-form-item>-->
<!--					</el-col>-->
<!--					<el-col class="text-center" :span="2">-->
<!--						<span class="text-gray-500">-</span>-->
<!--					</el-col>-->
<!--					<el-col :span="11">-->
<!--						<el-form-item prop="date2">-->
<!--							<el-time-picker-->
<!--									v-model="ruleForm.date2"-->
<!--									label="Pick a time"-->
<!--									placeholder="Pick a time"-->
<!--									style="width: 100%"-->
<!--							/>-->
<!--						</el-form-item>-->
<!--					</el-col>-->
<!--				</el-form-item>-->
<!--				<el-form-item label="Instant delivery" prop="delivery">-->
<!--					<el-switch v-model="ruleForm.delivery" />-->
<!--				</el-form-item>-->
<!--				<el-form-item label="Activity type" prop="type">-->
<!--					<el-checkbox-group v-model="ruleForm.type">-->
<!--						<el-checkbox value="Online activities" name="type">-->
<!--							Online activities-->
<!--						</el-checkbox>-->
<!--						<el-checkbox value="Promotion activities" name="type">-->
<!--							Promotion activities-->
<!--						</el-checkbox>-->
<!--						<el-checkbox value="Offline activities" name="type">-->
<!--							Offline activities-->
<!--						</el-checkbox>-->
<!--						<el-checkbox value="Simple brand exposure" name="type">-->
<!--							Simple brand exposure-->
<!--						</el-checkbox>-->
<!--					</el-checkbox-group>-->
<!--				</el-form-item>-->
<!--				<el-form-item label="Resources" prop="resource">-->
<!--					<el-radio-group v-model="ruleForm.resource">-->
<!--						<el-radio value="Sponsorship">Sponsorship</el-radio>-->
<!--						<el-radio value="Venue">Venue</el-radio>-->
<!--					</el-radio-group>-->
<!--				</el-form-item>-->
<!--				<el-form-item label="Activity form" prop="desc">-->
<!--					<el-input v-model="ruleForm.desc" type="textarea" />-->
<!--				</el-form-item>-->
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

<!--<script setup lang="ts" name="funCountup">-->
<!--import { reactive, onMounted, nextTick, ref } from 'vue';-->
<!--import { CountUp } from 'countup.js';-->

<!--// 定义变量内容-->
<!--const topCardItemRefs = ref<RefType[]>([]);-->
<!--const state = reactive({-->
<!--	topCardItemList: [-->
<!--		{-->
<!--			title: '今日访问人数',-->
<!--			titleNum: '123',-->
<!--			tip: '在场人数',-->
<!--			tipNum: '911',-->
<!--			color: '&#45;&#45;el-color-primary',-->
<!--			iconColor: '#ffcb47',-->
<!--			icon: 'iconfont icon-jinridaiban',-->
<!--		},-->
<!--		{-->
<!--			title: '实验室总数',-->
<!--			titleNum: '123',-->
<!--			tip: '使用中',-->
<!--			tipNum: '611',-->
<!--			color: '&#45;&#45;el-color-success',-->
<!--			iconColor: '#70cf41',-->
<!--			icon: 'iconfont icon-AIshiyanshi',-->
<!--		},-->
<!--		{-->
<!--			title: '申请人数（月）',-->
<!--			titleNum: '123',-->
<!--			tip: '通过人数',-->
<!--			tipNum: '911',-->
<!--			color: '&#45;&#45;el-color-warning',-->
<!--			iconColor: '#dfae64',-->
<!--			icon: 'iconfont icon-shenqingkaiban',-->
<!--		},-->
<!--		{-->
<!--			title: '销售情况',-->
<!--			titleNum: '123',-->
<!--			tip: '销售数',-->
<!--			tipNum: '911',-->
<!--			color: '&#45;&#45;el-color-danger',-->
<!--			iconColor: '#e56565',-->
<!--			icon: 'iconfont icon-ditu',-->
<!--		},-->
<!--	],-->
<!--});-->

<!--// 初始化数字滚动-->
<!--const initNumCountUp = () => {-->
<!--	nextTick(() => {-->
<!--		topCardItemRefs.value.forEach((v: HTMLDivElement) => {-->
<!--			new CountUp(v.querySelector('.countup-card-item-title-num') as HTMLDivElement, Math.random() * 10000).start();-->
<!--			new CountUp(v.querySelector('.countup-card-item-tip-num') as HTMLDivElement, Math.random() * 1000).start();-->
<!--		});-->
<!--	});-->
<!--};-->
<!--// 重置/刷新数值-->
<!--// 页面加载时-->
<!--onMounted(() => {-->
<!--	initNumCountUp();-->
<!--});-->
<!--</script>-->

<!--<style scoped lang="scss">-->
<!--.countup-card-item {-->
<!--	width: 100%;-->
<!--	height: 103px;-->
<!--	background: var(&#45;&#45;el-text-color-secondary);-->
<!--	border-radius: 4px;-->
<!--	transition: all ease 0.3s;-->
<!--	&:hover {-->
<!--		box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);-->
<!--		transition: all ease 0.3s;-->
<!--	}-->
<!--}-->
<!--.countup-card-item-box {-->
<!--	display: flex;-->
<!--	align-items: center;-->
<!--	position: relative;-->
<!--	overflow: hidden;-->
<!--	&:hover {-->
<!--		i {-->
<!--			right: 0px !important;-->
<!--			bottom: 0px !important;-->
<!--			transition: all ease 0.3s;-->
<!--		}-->
<!--	}-->
<!--	i {-->
<!--		position: absolute;-->
<!--		right: -10px;-->
<!--		bottom: -10px;-->
<!--		font-size: 70px;-->
<!--		transform: rotate(-30deg);-->
<!--		transition: all ease 0.3s;-->
<!--	}-->
<!--	.countup-card-item-flex {-->
<!--		padding: 0 20px;-->
<!--		color: var(&#45;&#45;el-color-white);-->
<!--		.countup-card-item-title,-->
<!--		.countup-card-item-tip {-->
<!--			font-size: 13px;-->
<!--		}-->
<!--		.countup-card-item-title-num {-->
<!--			font-size: 18px;-->
<!--		}-->
<!--		.countup-card-item-tip-num {-->
<!--			font-size: 13px;-->
<!--		}-->
<!--	}-->
<!--}-->
<!--</style>-->
<script lang="ts" setup>
import { reactive, ref } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'

interface RuleForm {
	name: string
	region: string
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
	name: '请输入',
	region: '',
	count: '',
	date1: '',
	date2: '',
	delivery: false,
	type: [],
	resource: '',
	desc: '',
})

const rules = reactive<FormRules<RuleForm>>({
	name: [
		{ required: true, message: 'Please input Activity name', trigger: 'blur' },
		{ min: 9, max: 80, message: 'Length should be 9 to 80', trigger: 'blur' },
	],
	region: [
		{
			required: true,
			message: 'Please select Activity zone',
			trigger: 'change',
		},
	],
	// count: [
	// 	{
	// 		required: true,
	// 		message: 'Please select Activity count',
	// 		trigger: 'change',
	// 	},
	// ],
	// date1: [
	// 	{
	// 		type: 'date',
	// 		required: true,
	// 		message: 'Please pick a date',
	// 		trigger: 'change',
	// 	},
	// ],
	// date2: [
	// 	{
	// 		type: 'date',
	// 		required: true,
	// 		message: 'Please pick a time',
	// 		trigger: 'change',
	// 	},
	// ],
	// type: [
	// 	{
	// 		type: 'array',
	// 		required: true,
	// 		message: 'Please select at least one activity type',
	// 		trigger: 'change',
	// 	},
	// ],
	// resource: [
	// 	{
	// 		required: true,
	// 		message: 'Please select activity resource',
	// 		trigger: 'change',
	// 	},
	// ],
	// desc: [
	// 	{ required: true, message: 'Please input activity form', trigger: 'blur' },
	// ],
})

// const submitForm = async (formEl: FormInstance | undefined) => {
// 	if (!formEl) return
// 	await formEl.validate((valid, fields) => {
// 		if (valid) {
//
// 		} else {
//
// 		}
// 	})
// }

const resetForm = (formEl: FormInstance | undefined) => {
	if (!formEl) return
	formEl.resetFields()
}

const options = Array.from({ length: 10000 }).map((_, idx) => ({
	value: `${idx + 1}`,
	label: `${idx + 1}`,
}))
</script>