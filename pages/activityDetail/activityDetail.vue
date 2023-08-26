<template>
	<view>
		<view class="page-header">
			<view class="back">
				<uni-icons type="back" size="22" color="#fff" class="go-back" @click="goBack"></uni-icons>
				<text>返回</text>
			</view>
			<text class="act-title">HITwhLinker发布会</text>
			<view class="view-nums">
				<uni-icons type="eye" size="15" color="#fff" class="view-num" ></uni-icons>
				<text>5000</text>
			</view>
			<view class="act-person">
				<view>
				  <image src="https://cdn.pixabay.com/photo/2021/07/22/11/25/rabbit-6485072_1280.jpg" mode="aspectFill" class="radius" style="height: 40rpx;width: 40rpx;"></image>
				</view>
				<text class="person-name">HITwhLinker团队</text>
			</view>
		</view>
		<view class="page-body">
			<!-- <view class="img-like" @click="commentLike(item)">
				<image src="../../static/aixin.png" v-if="item.isLike == 0 || item.isLike == null"></image>
				<image src="../../static/aixin3.png" v-else></image>
				<text class="comment-like-num">{{ item.likeNums == 0 || item.likeNums == null ? '' : item.likeNums }}</text>
			</view> -->
			<!-- <view class="fa" :class="{'fa-heart': liked, 'fa-heart-o': !liked}" @click="toggleLike"></view>-->
			<!-- <view class="heart-icon" :class="liked ? 'liked' : ''" @tap="toggleLike"></view> -->
			<uni-icons type="heart" size="22" color="#ef5656" @click="toggleLike()" v-if="!liked"></uni-icons>
			<uni-icons type="heart-filled" size="22" color="#ef5656" @click="toggleLike()" v-else="liked"></uni-icons>
			    <text>{{ likeCount }}</text>
		</view>
	</view>
</template>

<script setup>
	import {
		ref,
		reactive,
		onMounted,
		computed,
		watch
	} from 'vue'
	import {
		onLoad,onInit
	} from '@dcloudio/uni-app'
	// import { sortBy } from 'lodash'
	// 返回标志
	const goBack = () => {
		uni.navigateBack({
			delta: 1
		})
	}
	var liked = ref(false)
	var likeCount = ref(0)
	const toggleLike = ()=> {
	  liked.value = !liked.value;
	  likeCount.value += liked.value ? 1 : -1;
	  console.log('liked',liked,'likeCount',likeCount);
	}
</script>

<style lang="scss">
	.page-header {
	  width: 100%;
	  height: 400rpx;
	  background-image: url("https://cdn.pixabay.com/photo/2020/05/19/13/35/cartoon-5190860_1280.jpg");
	  background-size: 100% ;
	  background-position: center center; /* 或者根据需要进行调整 */
	  position: relative;
	  .back{
		  position: absolute;
		  display: flex;
		  top: 20rpx;
		  left: 20rpx;
		  color: #fff;
		  font-size: 30rpx;
	  }
	  .act-title {
		  position: absolute;
		  display: flex;
		  top: 200rpx;
		  left: 30rpx;
		  color: #fff;
		  font-size: 45rpx;
		  font-weight: 500;
	  }
	  .view-nums{
		  opacity: 0.9;
		  font-size: 15rpx;
		  color: #fff;
		  position: absolute;
		  display: flex;
		  right: 40rpx;
		  bottom: 30rpx;
		  .view-num {
			  margin-right: 5rpx;
		  }
	  }
	  .act-person {
		  position: absolute;
		  display: flex;
		  left: 40rpx;
		  bottom: 30rpx;
		  .radius {
			  border-radius: 100%;
			  margin-right: 5rpx;
		  }
		  .person-name{
			  color: #fff;
			  opacity: 0.8;
		  }
	  }
	}
	// .img-like {
	// 	image {
	// 		display: block;
	// 		width: 50rpx;
	// 		height: 50rpx;
	// 		margin-top: 20rpx;
	// 	}
	// 	.comment-like-num {
	// 		display: inline-block;
	// 		width: 50rpx;
	// 		text-align: center;
	// 	}
	// }

</style>
