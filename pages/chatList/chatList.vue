<template>
	<view class="chat">
		<!-- 头部 -->
		<view class="header">
			<text class="title">Student Buddy</text>
			<view class="tool">
				<text class="iconfont icon-tianjiahaoyou icon"></text>
				<text class="iconfont icon-danlieliebiao icon"></text>
			</view>
		</view>
		<!-- 所有好友列表 -->
		<scroll-view class="content" scroll-y="true"> 
			<ul>
				<li v-for="(chat, index) in chat_views" :key="index" class="chat-view" @click="handleClick(chat)">
					<image src="@/static/head.jpeg" mode="aspectFill" class="chat-img"></image>
					<view class="chat-content">
						<text class="text-name">{{chat.name}}</text>
						<text class="text-word">{{chat.last_word}}</text>
					</view>
					<view class="chat-date">
						<text>{{chat.last_word_date}}</text>
					</view>
				</li>
			</ul>
		</scroll-view>
	</view>
</template>

<script setup>
import {reactive, ref} from 'vue'

const chat_views = reactive([
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	},
	{
		tag:"小助手",
		name:"哈小助",
		head_img_url:"@/static/头像.jpeg",
		last_word:"hello, 我是你的小助手",
		last_word_date:"星期三"
	}
]);

// 点击跳转聊天界面
const handleClick = (chat) => {
	uni.navigateTo({
		url:`/pages/chat/chat?name=${chat.name}`
	})
}

</script>

<style lang="scss" scoped>
.header {
	display: flex;
	justify-content: space-between;
	height: 10vh;
	line-height: 10vh;
	padding: 0 30rpx;
	border-bottom: 1px solid rgb(244, 244, 244);
	.title {
		font-size: 22px;
		font-weight: 600;
	}
	.tool {
		.icon {
			margin-left: 20rpx;
			font-size: 22px;
		}
		
	}
}
.content {
	height: calc(90vh - var(--window-bottom));
	width: 750rpx;
	ul {
		padding: 0;
	}
	ul li {
		box-sizing: border-box;
		list-style: none;
	}
	.chat-view {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		width: 100vw;
		height: 64px;
		padding: 3vw;
		border-bottom: 1px solid rgb(244, 244, 244);
		.chat-img {
			width: 10vw;
			height: 10vw;
		}
		.chat-content {
			display: flex;
			flex-direction: column;
			width: 65vw;
			.text-name {
				line-height: 22px;
				font-size: 16px;
			}
			.text-word {
				line-height: 22px;
				font-size: 13px;
				color: $uni-text-color-grey;
			}
		}
		.chat-date {
			width: 10vw;
			font-size: 12px;
			color: $uni-text-color-grey;
		}
	}
}

</style>
