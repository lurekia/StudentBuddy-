<template>
	<view>
		<view class="topbar">
			<view class="topbar-content">
				活动列表
			</view>
			<uni-icons type="back" size="30" color="#fff" class="go-back" @click="goBack"></uni-icons>
		</view>
		<view class="schedule-list">
			<!-- 头部 -->
			<view class="schedule-list-header">
				<view class="schedule-list-header-btn" @click="prevMonth">上个月</view>
				<view class="schedule-list-header-title">
					<uni-dateformat :date="currentDate" format="yyyy年M月" ref="currentDateShow"></uni-dateformat>
				</view>
				<view class="schedule-list-header-btn" @click="nextMonth">下个月</view>
				<!-- <view class="schedule-list-header-right"> -->
				<!-- <picker mode="selector" :range=" categories " @change="changeCategory">
		          <view class="schedule-list-header-category">{{ currentCategory }}</view>
		        </picker> -->
				<!-- view -->
				<!-- </view> -->
			</view>
			<!-- 标签 -->
			<uni-fab :pattern="tag_pattern" :content="tag_content" horizontal="right" vertical="bottom"
				direction="vertical" @trigger="tag_trigger"></uni-fab>
			<!-- 主体 -->
			<view class="schedule-list-body">
				<view class="schedule-list-date" v-for="(item_date,index_date) in schedule" :key="index_date">
					<view class="schedule-list-date-header">{{item_date.date}}</view>
					<view class="schedule-list-date-body">
						<view class="schedule-list-date-item" v-for="(item_time, index_time) in item_date.content" :key="index_time">
							<view class="item-time">{{item_time.time}}</view>
							<view class="item-tag iconfont icon-yuan" :style="{color:tagToColor(item_time.tag)}">
								
							</view>
							<view class="item-title">{{item_time.title}}</view>
						</view>
					</view>
					
				</view>
			</view>
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
	// 返回标志
	const goBack = () => {
		uni.navigateBack({
			delta: 1
		})
	}
	
	// 头部时间
	const currentDate = reactive(new Date())
	const currentDateShow = ref("");
	const prevMonth = () => {
		console.log(currentDate);
		currentDate.setMonth(currentDate.getMonth() - 1)
		// 动态修改
		// console.log(currentDateShow.value);
		// currentDateShow.value.date = currentDate;
	}
	
	const nextMonth = () => {
		console.log(currentDate);
		currentDate.setMonth(currentDate.getMonth() + 1)
		// currentDateShow.value.date = currentDate;
	}

	// 标签选择
	const tag_pattern = {
		color: '#7A7E83',
		backgroundColor: '#fff',
		selectedColor: '#007AFF',
		buttonColor: '#007AFF',
		iconColor: '#fff'
	}
	const tag_content = reactive([{
			text: '全部',
			active: true,
			iconPath: '/static/便签1.svg',
			selectedIconPath: '/static/便签1.svg',
		},
		{
			text: '讲座报告',
			active: false,
			iconPath: '/static/便签2.svg',
			selectedIconPath: '/static/便签2.svg',
		},
		{
			text: '会议',
			active: false,
			iconPath: '/static/便签3.svg',
			selectedIconPath: '/static/便签3.svg',
		},
		{
			text: '考试答辩',
			active: false,
			iconPath: '/static/便签4.svg',
			selectedIconPath: '/static/便签4.svg',
		},
		{
			text: '主题活动',
			active: false,
			iconPath: '/static/便签5.svg',
			selectedIconPath: '/static/便签5.svg',
		},
		{
			text: '电影演出',
			active: false,
			iconPath: '/static/便签6.svg',
			selectedIconPath: '/static/便签6.svg',
		},

		{
			text: '竞赛',
			active: false,
			iconPath: '/static/便签7.svg',
			selectedIconPath: '/static/便签7.svg',
		},
		{
			text: '其他',
			active: false,
			iconPath: '/static/便签1.svg',
			selectedIconPath: '/static/便签1.svg',
		},
	])
	const selectedTag = ref('全部')
	const tag_colors = ['#333333','#337ab7','#f0ad4e','#5bc0de','#d9534f','#339900','#663366'];
	const tag_trigger = (e) => {
		// console.log(e);
		tag_content.forEach(tag => {
			tag.active = false;
		})
		tag_content[e.index].active = true;
		selectedTag.value = tag_content[e.index].text;
		console.log(selectedTag.value);
	}

	// const filterSchedule = computed(() => {
	// 	const year = displayYear.value
	// 	const month = displayMonth.value
	// 	const monthSchedule = schedule.filter(item => {
	// 		const date = new Date(item.date)
	// 		return date.getFullYear() === year && date.getMonth() + 1 === month
	// 	})

	// 	if (selectedTag.value !== '全部') {
	// 		monthSchedule = monthSchedule.filter(item => item.tag === selectedTag.value)
	// 	}

	// 	const daySchedule = monthSchedule.reduce((acc, item) => {
	// 		const date = item.date.split('-').pop()
	// 		if (!acc[date]) {
	// 			acc[date] = []
	// 		}
	// 		acc[date].push(item)
	// 		return acc
	// 	}, {})

	// 	return Object.entries(daySchedule).map(([date, items]) => ({
	// 		date,
	// 		items
	// 	}))
	// })

	// 展示列表
	const schedule = reactive([
		{
			date: '2023-07-08',
			content: [
				{
					title: '去比赛',
					time: '08:00',
					tag: '竞赛',
				},
				{
					title: '去比赛',
					time: '10:00',
					tag: '讲座报告',
				}
			]
		},
		{
			date: '2023-07-09',
			content: [
				{
					title: '去比赛',
					time: '08:00',
					tag: '竞赛',
				}
			]
		},
		{
			date: '2023-07-10',
			content: [
				{
					title: '去比赛',
					time: '08:00',
					tag: '会议',
				},
				{
					title: '去比赛',
					time: '10:00',
					tag: '考前答辩',
				}
			]
		},
	])
	const tagToColor = (tag_name) => {
		for(var i=0;i<tag_content.length;i++) {
			console.log(tag_content[i]);
			if(tag_content[i].text == tag_name)
				return tag_colors[i];
		}
	}
</script>

<style lang="scss">
	.topbar {
		width: 100%;
		height: 80rpx;
		line-height: 80rpx;
		color: #fff;
		background-color: #e85353;
		display: flex;
		position: relative;
		top: 0;
		left: 0;
		justify-content: center;

		.go-back {
			position: absolute;
			top: 0rpx;
			left: 20rpx;
			z-index: 99;
		}
	}

	.schedule-list {
		height: 100%;
		display: flex;
		flex-direction: column;
	}

	.schedule-list-header {
		width: 100vw;
		height: 88rpx;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		background-color: #ffffff;
		font-size: 24px;
		box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.1);
		padding: 0 32rpx;
	}

	.schedule-list-header-btn {
		font-size: 16px;
		color: #333333;
		cursor: pointer;
	}
	.schedule-list-body {
		display: flex;
		flex-direction: column;
		width: 100vw;
		padding: 0 20rpx;
		border-left: 1px solid rgb(244,244,244);
		.schedule-list-date-header {
			height: 75rpx;
			line-height: 75rpx;
			padding: 0 25px;
			font-weight: 600;
			background-color: #eee;
		}
		.schedule-list-date-item {
			display: flex;
			flex-direction: row;
			height: 75rpx;
			line-height: 75rpx;
			padding: 0 20px;
			border: 1px solid rgb(244,244,244);
			.item-tag {
				margin-left: 40rpx;
			}
			.item-title {
				margin-left: 20rpx;
			}
		}
	}
</style>