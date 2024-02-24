<template>
	<view class="container">
		<view class="leave_info">
			<text>还剩{{coins}}个硬币</text>
			<text>已种{{trees.length}}棵树</text>
		</view>
		<image src="/static/img/treeback.jpg" class="grassland"></image>
		<view class="tree-container">
			<image v-for="(tree, index) in trees" :key="index" src="/static/img/tree.png" class="tree"
				:style="{left: tree.x + 'px', top: tree.y + 'px'}"></image>
		</view>
		<button class="plant-tree-btn" @click="plantTree">种一棵树（需要{{treeCost}}币）</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				trees: [],
				coins: 10, // 假设用户有10个币
				treeCost: 1, // 每棵树的成本
				screenWidth: 0,
				screenHeight: 0
			};
		},
		mounted() {
			this.getScreenSize();
		},
		methods: {
			getScreenSize() {
				const res = uni.getSystemInfoSync();
				this.screenWidth = res.windowWidth;
				this.screenHeight = res.windowHeight;
			},
			plantTree() {
				if (this.coins >= this.treeCost) {
					const newTree = {
						x: Math.random() * this.screenWidth, // 横坐标随机
						y: (this.screenHeight / 2) - 50 + Math.random() * 100 // 纵坐标在屏幕上下中间区间
					};
					this.trees.push(newTree);
					this.coins -= this.treeCost; // 扣除币
				} else {
					uni.showToast({
						title: '币不足',
						icon: 'none'
					});
				}
			}
		}
	};
</script>

<style>
	.container {
		position: relative;
		width: 100%;
		height: 100vh;
		overflow: hidden;

	}
	.leave_info {
		display: flex;
		flex-direction: column;
		position: absolute;
		left: 2%;
		top: 5%;
		z-index: 9999;
	}

	.grassland {
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
	}

	.tree-container {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}

	.tree {
		position: absolute;
		width: 50px;
		/* 树的大小 */
		height: 50px;
	}

	.plant-tree-btn {
		position: fixed;
		bottom: 20px;
		left: 50%;
		width: 80%;
		transform: translateX(-50%);
		padding: 10px 20px;
		background-color: #4CAF50;
		color: white;
		border: none;
		border-radius: 5px;
	}
</style>