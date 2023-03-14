<template>
	<view class="content">
		<u-form labelPosition="left" :model="model1" :rules="rules" ref="form1">
			<u-form-item label="网址" prop="userInfo.website" borderBottom ref="item1">
				<u-input class="inptWeb" v-model="model1.userInfo.website" placeholder="请填写网址"></u-input>
			</u-form-item>
		
			<u-form-item label="域名" prop="userInfo.realmName" borderBottom ref="item1">
				<u-input class="inptWeb" v-model="model1.userInfo.realmName" placeholder="请填写域名"></u-input>
			</u-form-item>
		</u-form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
               rules: {
               	'userInfo.website': {
               		type: 'string',
               		required: true,
               		message: '请填写网址',
               		trigger: ['blur', 'change']
               	},
               	'userInfo.realmName': {
               		type: 'string',
               		required: true,
               		message: '请填写域名',
               		trigger: ['blur', 'change']
               	},
               
               },
				model1: {
					userInfo: {
						website: '',
				        realmName:''
					},
				},
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="scss">
    .inptWeb {
       border-width: 1px !important;
           border-color: #f00 !important;
           border-style: solid;
    }
</style>
