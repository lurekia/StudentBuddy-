<template>
	<view class="chat">
		<!-- 主要聊天页面 -->
		
		<scroll-view class="content" scroll-y="true" :scroll-into-view="`msg${msgs.length-1}`" :scroll-with-animation="true">
			<view class="msg-list">
				<view class="msg-item" :id="`msg${index}`" v-for="(msg, index) in msgs" :key="msg.time">
					<left-chat v-if="msg.left" :text="msg.text" :head_img_url="img_url"></left-chat>
					<right-chat v-else :text="msg.text" :head_img_url="img_url"></right-chat>
				</view>
			</view>
		</scroll-view>
		<view class="bottom-input">
			<text class="iconfont icon-yuyin icon"></text>
			
			<view class="textarea-container">
				<textarea auto-height fixed="true" confirm-type="send" v-model="input" @confirm="submit" />
			</view>
			<text class="iconfont icon-luyin icon"></text>
			<text class="iconfont icon-jiahao icon"></text>
		</view>
	</view>
</template>

<script setup>
	import {
		ref,
		reactive
	} from 'vue'
	import {
		onLoad
	} from '@dcloudio/uni-app'
import leftChat from '@/components/leftChat.vue'
import rightChat from '@/components/rightChat.vue'
	onLoad((obj) => {
		console.log(obj.name);
		uni.setNavigationBarTitle({
			title: obj.name
		})
	})
	const msgs = reactive([
		{
			left: false,
			text: '你是谁',
			time: "1"
		},
		{
			left: true,
			text: '你是谁',
			time: "2"
		},
		{
			left: false,
			text: '你是谁',
			time: "3"
		},
		{
			left: true,
			text: '你是谁',
			time: "4"
		},
		{
			left: false,
			text: '你是谁',
			time: "5"
		},
		{
			left: true,
			text: '你是谁',
			time: "6"
		},
		{
			left: false,
			text: '你是谁',
			time: "7"
		},
		{
			left: true,
			text: '你是谁',
			time: "8"
		},
		{
			left: false,
			text: '你是谁',
			time: "9"
		},
		{
			left: true,
			text: '你是谁',
			time: "10"
		},
		{
			left: false,
			text: '你是谁',
			time: "111"
		},
		{
			left: true,
			text: '你是谁',
			time: "12"
		},
		{
			left: false,
			text: '你是谁我是谁，你是谁我是谁，你是谁我是谁你是谁我是谁你是谁我是谁你是谁我是谁你是谁我是谁你是谁我是谁',
			time: "13"
		},
		{
			left: true,
			text: '你是谁',
			time: "14"
		},
	]);
	const scrollTop = ref(0)
	const input = ref("");
	const img_url = "../../static/head.jpeg"
	const scrool_to_bottom = () => {
		
	}
	const submit = function() {
		if (input.value === "") return;
		msgs.push({
			left: false,
			text: input.value,
			time: new Date().getTime(),
		});
		// 此处会有异步询问和错误处理
		const receiveText = "不知道";

		msgs.push({
			left: true,
			text: receiveText,
			time: new Date().getTime(),
		});
		input.value = "";
		last_item.value = 'msg' + (msgs.length - 1)
		console.log(msgs);
		console.log(last_item.value);
	}
</script>

<style lang="scss" scoped>
	.chat {
		width: 100vw;
		height: calc(100vh - 44px);
	}
	.content {
		box-sizing: border-box;
		height: calc(90vh - 44px);
		padding: 0 10px;
	}
	
	.bottom-input {
		display: flex;
		align-items: flex-end;
		position: fixed;
		bottom: 0px;
		width: 100vw;
		height: 50px;
		background-color: $uni-bg-color-grey;
		padding: 10px;
		.textarea-container {
			flex-grow: 1;
			height: 30px;
			line-height: 30px;
			margin-left: 20rpx;
			background-color: #ffffff;
			textarea {
				width: calc(100vw - 146px);
				background-color: #ffffff;
			}
		}
		.icon {
			margin-left: 20rpx;
			font-size: 24px;
			// color: $uni-bg-color-grey;
		}
	}
</style>