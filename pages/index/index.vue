<template>
	<view class="content">
		<view class="tab-wrapper">
			<easy-tab-bar
				ref="tabBar"
				:data="tab"
				:value="currentValue"
				@tabClick="tabClick"
			>
			</easy-tab-bar>
		</view>
		<view class="tab-swiper">
			<swiper
				@transition="transition"
				duration="200"
				:current="currentIndex"
				@change="change"
				easing-function="linear"
			>
				<swiper-item
					v-for="item in swiper"
					:style="{ backgroundColor: item.background }"
					:key="item.label"
				>
					<text>{{ item.name }}</text>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			tab: [
				{
					label: 'Home',
					icon: 'cubeic-home',
					value: 0
				},
				{
					label: 'Like',
					icon: 'cubeic-like',
					value: 1
				},
				{
					label: 'Vip',
					icon: 'cubeic-vip',
					value: 2
				},
				{
					label: 'Me',
					icon: 'cubeic-person',
					value: 3
				}
			],
			swiper: [
				{
					name: 'Home',
					background: 'black'
				},
				{
					name: 'Like',
					background: 'yellow'
				},
				{
					name: 'Vip',
					background: 'blue'
				},
				{
					name: 'Me',
					background: 'pink'
				}
			],
			currentValue: 0,
			currentIndex: 0
		};
	},
	mounted() {
		setTimeout(() => {
			console.log(this.$refs.swiper)
		}, 1000)
	},
	methods: {
		tabClick(value) {
			this.currentValue = Number(value);
			this.currentIndex = Number(value);
		},
		change(e) {
			console.log('改变了change')
			this.currentValue = Number(e.detail.current);
		},
		transition(e) {
			let { dx } = e.detail;
			dx = Math.abs(dx)
			this.$refs.tabBar.setSliderTransform(dx);
		}
	}
};
</script>

<style>
.content {
	position: fixed;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	width: 100%;
	margin: 0;
}

.tab-wrapper {
	width: 100%;
	height: 40px;
}
.tab-swiper {
	height: calc(100% - 40px);
}

swiper {
	height: 100%;
	text-align: center;
}

swiper-item {
	display: flex;
	align-items: center;
	justify-content: center;
	color: #ffffff;
	font-size: 24px;
	font-weight: bold;
}
</style>
