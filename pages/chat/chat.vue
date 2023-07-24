<template>
	<view class="chat">
		<!-- 主要聊天页面 -->
		
		<scroll-view class="content" scroll-y="true" :scroll-into-view="`msg${msgs.length-1}`" :scroll-with-animation="true">
			<view class="msg-list">
				<view class="msg-item" :id="`msg${index}`" v-for="(msg, index) in msgs" :key="msg.time">
					<left-chat v-if="msg.left" :msg="msg" :head_img_url="img_url"></left-chat>
					<right-chat v-else :msg="msg" :head_img_url="img_url"></right-chat>
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
			left: true,
			content: `	# 你是谁\n- 呵呵哒\n## 一人我饮酒醉`,
			time: "1"
		},
		{
			left: false,
			content: `# 你是谁 
					- 呵呵哒 
					## 一人我饮酒醉`,
			time: "2"
		},
		{
			left: false,
			content: ' 你是谁',
			time: "3"
		},
		{
			left: true,
			content: ' 你是谁',
			time: "4"
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
			content: input.value,
			time: new Date().getTime(),
		});
		// 此处会有异步询问和错误处理
		const receiveText = "不知道";

		msgs.push({
			left: true,
			content: receiveText,
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
		background-color: rgb(227,227,227);
	}
	.content {
		box-sizing: border-box;
		height: calc(90vh - 44px);
		padding: 0 10px;
	}
	.msg-list {
		margin-top: 20rpx;
	}
	.msg-item {
		margin-top: 10rpx;
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