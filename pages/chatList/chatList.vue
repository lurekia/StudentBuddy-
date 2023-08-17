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
		<!-- <scroll-view class="content" scroll-y="true"> 
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
		</scroll-view> -->
		<unicloud-db ref="udb" v-slot:default="{data, loading, error, options}" :options="options" collection="server_list" orderby="last_word_date desc">
		  <view v-if="error">{{error.message}}</view>
		  <view v-else-if="loading">
		    <uni-load-more :contentText="loadMore" status="loading"></uni-load-more>
		  </view>
		  <view v-else-if="data">
			<uni-list>
				<uni-list :border="true">
					<uni-list-chat 
					 v-for="chat in data" 
					 :key="chat._id"
					:title="chat.name" 
					:avatar="chat.avatar" 
					:note="formatWord(chat.last_word)" 
					:time="formatDate(chat.last_word_date)" 
					 :clickable="true"
					@click="handleClick(chat)"
					></uni-list-chat>
				</uni-list>
			</uni-list>
		  </view>
		</unicloud-db>
		
	</view>
</template>

<script setup>
import {reactive, ref} from 'vue'
import {
		onLoad
	} from '@dcloudio/uni-app'
let chat_views = reactive([]);
const udb = ref()
// 点击跳转聊天界面
const handleClick = (chat) => {
	console.log(chat);
	uni.navigateTo({
		url:`/pages/chat/chat?name=${chat.name}&url=${chat.avatar}&id=${chat._id}`, // 传递url感觉有点不好
		
	})
	console.log("父组件中：",udb);
	// console.log("传输信息给下一个");
	// uni.$emit('listToChat',chat.avatar)
}
const formatDate = (time) => {
	const someDate = new Date(time);
	return someDate.toLocaleDateString();
}
const formatWord = (text) => {
	if(text.length <= 20) {
		return text;
	}
	else
		return text.slice(0,17) + "...";
}
// onLoad(() => {
// 	const db = uniCloud.database();
// 	db.collection('server_list').get().then((res) => {
// 			chat_views = res.result.data
// 			console.log("获取用户信息:",chat_views);
// 		})
// 		.catch((error) => {
// 			console.log(error);
// 		})
// })
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
