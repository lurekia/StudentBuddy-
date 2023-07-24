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
		      <view class="schedule-list-header-left">
		        <view class="schedule-list-header-btn" @click="prevMonth">上个月</view>
		        <view class="schedule-list-header-title">{{ displayYear }}年{{ displayMonth }}月</view>
		        <view class="schedule-list-header-btn" @click="nextMonth">下个月</view>
		      </view>
		      <!-- <view class="schedule-list-header-right"> -->
		        <!-- <picker mode="selector" :range=" categories " @change="changeCategory">
		          <view class="schedule-list-header-category">{{ currentCategory }}</view>
		        </picker> -->
				<!-- view
		      </view> -->
			  <view v-for="tag in tags" :key="tag" @click="selectTag(tag)">
			  	{{tag}}
			  </view>
		    </view>
		    <!-- 主体 -->
		    <view class="schedule-list-body">
		      <view class="schedule-list-days">
		        <!-- <view class="schedule-list-day" v-for="(day, index) in days" :key="index"> -->
		        <view class="schedule-list-day" v-for="day in filterSchedule" :key="day.date">
		          <view class="schedule-list-day-header">{{ day.date }}</view>
		          <view class="schedule-list-day-body">
		            <!-- <view class="schedule-list-schedule" v-for="(schedule, index) in schedules[day]" :key="index">
		              <view class="schedule-list-schedule-time">{{ schedule.time }}</view>
		              <view class="schedule-list-schedule-title">{{ schedule.title }}</view>
		            </view> -->
					<view class="schedule-list-schedule" v-for="item in day.items" :key="item.title">
					  <view class="schedule-list-schedule-time">{{ item.time }}</view>
					  <view class="schedule-list-schedule-title">{{ item.title }}</view>
					</view>
		          </view>
		        </view>
		      </view>
		    </view>
		  </view>
	</view>
</template>

<script setup>
	const goBack = ()=>{
		uni.navigateBack({
			delta:1
		})
	}
	import { ref, reactive, onMounted,computed, watch } from 'vue'
	const schedule = reactive([
	  {
	    title: '去比赛',
	    date: '2023-07-08',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-02',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-07',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-11',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-08',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-08',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-18',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-08',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  {
	    title: '去比赛',
	    date: '2023-07-20',
	    time: '08:00',
	    tag: '竞赛',
	  },
	  // 更多的数据...
	])
	
	const currentDate = ref(new Date())
	const selectedTag = ref('全部')
	
	const displayYear = computed(() => currentDate.value.getFullYear())
	const displayMonth = computed(() => currentDate.value.getMonth() + 1)
	
	const tags = ['讲座报告', '会议', '考试答辩', '主题活动', '电影演出', '竞赛', '其他', '全部']
	
	const filterSchedule = computed(() => {
	  const year = displayYear.value
	  const month = displayMonth.value
	  const monthSchedule = schedule.filter(item => {
	    const date = new Date(item.date)
	    return date.getFullYear() === year && date.getMonth() + 1 === month
	  })
	
	  if (selectedTag.value !== '全部') {
	    monthSchedule = monthSchedule.filter(item => item.tag === selectedTag.value)
	  }
	
	  const daySchedule = monthSchedule.reduce((acc, item) => {
	    const date = item.date.split('-').pop()
	    if (!acc[date]) {
	      acc[date] = []
	    }
	    acc[date].push(item)
	    return acc
	  }, {})
	
	  return Object.entries(daySchedule).map(([date, items]) => ({ date, items }))
	})
	
	const prevMonth = () => {
	  currentDate.value.setMonth(currentDate.value.getMonth() - 1)
	}
	
	const nextMonth = () => {
	  currentDate.value.setMonth(currentDate.value.getMonth() + 1)
	}
	
	const selectTag = (tag) => {
	  selectedTag.value = tag
	}
	// // 当前的年份和月份
	//     const currentDate = new Date()
	//     const year = ref(currentDate.getFullYear())
	//     const month = ref(currentDate.getMonth() + 1)
	// // 日程列表数据
	// const schedules = reactive({
	//   '2023-7-1': [
	//     { time: '10:00', title: '参观博物馆', tag: '主题活动' },
	//     { time: '14:00', title: '学术报告', tag: '讲座报告' },
	//     { time: '16:00', title: '开会', tag: '会议' },
	//   ],
	//   '2023-7-2': [
	//     { time: '9:00', title: '考试', tag: '考试答辩' },
	//     { time: '14:00', title: '比赛', tag: '竞赛' },
	//     { time: '19:00', title: '看电影', tag: '电影演出' },
	//   ],
	//   '2023-7-3': [
	//     { time: '8:00', title: '健身', tag: '其他' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '18:00', title: '聚餐', tag: '其他' },
	//   ],
	//   '2023-7-4': [
	//     { time: '15:00', title: '学习', tag: '其他' },
	//     { time: '19:00', title: '打球', tag: '其他' },
	//   ],
	//   '2023-7-5': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-6': [
	//     { time: '10:00', title: '旅游', tag: '主题活动' },
	//     { time: '14:00', title: '会议', tag: '会议' },
	//     { time: '19:00', title: '吃火锅', tag: '其他' },
	//   ],
	//   '2023-7-7': [
	//     { time: '8:00', title: '跑步', tag: '其他' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '15:00', title: '看比赛', tag: '竞赛' },
	//   ],
	//   '2023-7-8': [
	//     { time: '9:00', title: '去比赛', tag: '竞赛' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '15:00', title: '考试', tag: '考试答辩' },
	//     { time: '18:00', title: '聚餐', tag: '其他' },
	//   ],
	//   '2023-7-9': [
	//     { time: '10:00', title: '旅游', tag: '主题活动' },
	//     { time: '14:00', title: '学术报告', tag: '讲座报告' },
	//     { time: '16:00', title: '开会', tag: '会议' },
	//   ],
	//   '2023-7-10': [
	//     { time: '9:00', title: '考试', tag: '考试答辩' },
	//     { time: '14:00', title: '比赛', tag: '竞赛' },
	//     { time: '19:00', title: '看电影', tag: '电影演出' },
	//   ],
	//   '2023-7-11': [
	//     { time: '8:00', title: '健身', tag: '其他' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '18:00', title: '聚餐', tag: '其他' },
	//   ],
	//   '2023-7-12': [
	//     { time: '15:00', title: '学习', tag: '其他' },
	//     { time: '19:00', title: '打球', tag: '其他' },
	//   ],
	//   '2023-7-13': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-14': [
	//     { time: '10:00', title: '旅游', tag: '主题活动' },
	//     { time: '14:00', title: '会议', tag: '会议' },
	//     { time: '19:00', title: '吃火锅', tag: '其他' },
	//   ],
	//   '2023-7-15': [
	//     { time: '8:00', title: '跑步', tag: '其他' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '15:00', title: '看比赛', tag: '竞赛' },
	//   ],
	//   '2023-7-16': [
	//     { time: '9:00', title: '去比赛', tag: '竞赛' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '15:00', title: '考试', tag: '考试答辩' },
	//     { time: '18:00', title: '聚餐', tag: '其他' },
	//   ],
	//   '2023-7-17': [
	//     { time: '10:00', title: '旅游', tag: '主题活动' },
	//     { time: '14:00', title: '学术报告', tag: '讲座报告' },
	//     { time: '16:00', title: '开会', tag: '会议' },
	//   ],
	//   '2023-7-18': [
	//     { time: '9:00', title: '考试', tag: '考试答辩' },
	//     { time: '14:00', title: '比赛', tag: '竞赛' },
	//     { time: '19:00', title: '看电影', tag: '电影演出' },
	//   ],
	//   '2023-7-19': [
	//     { time: '8:00', title: '健身', tag: '其他' },
	//     { time: '12:00', title: '午餐', tag: '其他' },
	//     { time: '18:00', title: '聚餐', tag: '其他' },
	//   ],
	//   '2023-7-20': [
	//     { time: '15:00', title: '学习', tag: '其他' },
	//     { time: '19:00', title: '打球', tag: '其他' },
	//   ],
	//   '2023-7-21': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-22': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-23': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-24': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-25': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-26': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-27': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-28': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-29': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-30': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	//   '2023-7-31': [
	//     { time: '16:00', title: '瑜伽', tag: '其他' },
	//     { time: '20:00', title: '听音乐会', tag: '电影演出' },
	//   ],
	// })
	//     // 当前选中的分类
	//     const currentCategory = ref('全部')
	//     const categories = ['全部', '讲座报告', '会议', '考试答辩', '主题活动', '电影演出', '竞赛', '其他']
	
	    
	//     // 获取当前月份的天数
	//     const getDaysInMonth = (year, month) => {
	//       return new Date(year, month, 0).getDate();
	//     }
	
	//     // 根据日期获取星期几
	//     const getDayOfWeek = (year, month, day) => {
	//       return new Date(year, month - 1, day).getDay();
	//     }
	
	//     // 根据年份和月份获取    当月的日程安排
	//     const getSchedulesInMonth = (year, month, category) => {
	//       const days = []
	//       const daysInMonth = getDaysInMonth(year, month)
	
	//       // 根据分类过滤日程安排
	//       if (category === '全部') {
	//         // 全部分类，返回所有日程安排
	//         for (let i = 1; i <= daysInMonth; i++) {
	//           const day = `${year}-${month}-${i}`;
	//           days.push(day);
	//           if (!schedules[day]) {
	//             schedules[day] = []
	//           }
	//         }
	//       } else {
	//         // 其他分类，只返回对应分类的日程安排
	//         for (let i = 1; i <= daysInMonth; i++) {
	//           const day = `${year}-${month}-${i}`;
	//           days.push(day);
	//           if (!schedules[day]) {
	//             schedules[day] = []
	//           }
	//           schedules[day] = schedules[day].filter(schedule => schedule.tag === category)
	//         }
	//       }
	
	//       // 根据日期和时间排序日程安排
	//       days.forEach(day => {
	//         schedules[day].sort((a, b) => {
	//           const timeA = new Date(`${day}T${a.time}`)
	//           const timeB = new Date(`${day}T${b.time}`)
	//           return timeA - timeB
	//         })
	//       })
	//       return days
	//     }
	
	//     // 更新日程列表
	//     const updateSchedules = () => {
	//       const days = getSchedulesInMonth(year.value, month.value, currentCategory.value)
	//       days.forEach(day => {
	//         const dayOfWeek = getDayOfWeek(year.value, month.value, day.split('-')[2])
	//         schedules[day].unshift({ time: '', title: '', tag: '' })
	//         for (let i = 0; i < dayOfWeek; i++) {
	//           schedules[day].unshift({ time: '', title: '', tag: '' })
	//         }
	//       })
	//     }
	//     // 切换月份
	//     const prevMonth = () => {
	//       if (month.value === 1) {
	//         year.value--
	//         month.value = 12
	//       } else {
	//         month.value--
	//       }
	//       updateSchedules()
	//     }
	
	//     const nextMonth = () => {
	//       if (month.value === 12) {
	//         year.value++
	//         month.value = 1
	//       } else {
	//         month.value++
	//       }
	//       updateSchedules()
	//     }
	
	//     // 切换分类
	//     const changeCategory = event => {
	//       currentCategory.value = categories[event.target.value]
	//       updateSchedules()
	//     }
	
	//     // 初始化日程列表
	//     onMounted(() => {
	//       updateSchedules()
	//     })
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
			z-index:99;
		}
	}
	.schedule-list {
	  height: 100%;
	  display: flex;
	  flex-direction: column;
	}
	
	.schedule-list-header {
	  height: 88rpx;
	  display: flex;
	  justify-content: space-between;
	  align-items: center;
	  background-color: #ffffff;
	  box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.1);
	  padding: 0 32rpx;
	}
	
	.schedule-list-header-left {
	  display: flex;
	  align-items: center;
	}
	
	.schedule-list-header-right {
	  display: flex;
	  align-items: center;
	}
	
	.schedule-list-header-btn {
	  font-size: 28rpx;
	  color: #333333;
	  cursor: pointer;
	}
</style>
