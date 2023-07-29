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
		if(input.value === "你好，小助手，我喜欢街舞，你能给我推荐一下相关社团吗？") {
			const receiveText = "你好，以下是根据您的爱好：街舞，自动匹配到合适的社团： 凤舞社。						详细介绍：作为哈工大威海星级社团评选六连冠   hiphop（嘻哈舞）、popping（机械舞）、breaking（地板舞）、Locking（锁舞）、Jazz（爵士）、urban（编舞）、kpop（男女韩舞）！我们一个不少，任您选择。";
		}
		if(input.value === "这个社团训练时间是什么时候呀？") {
			const receiveText = "每周一到周四21：25--22:20 紧张学习的晚自习过后，欢迎来大活101室";
		}
		if(input.value === "最近学校有哪些讲座可以参加？") {
			const receiveText = "【光电·讲座】高能激光尾波加速和增强型固体高次谐波实验研究进展及激光等离子体不稳定性及其抑制研究                                                            主讲人：陈民、翁苏明   主办单位：理学院光电科学系 地点：主楼H124   时间：2023年7月31日上午8:30-11:30  "       
			}

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