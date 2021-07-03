<template>
	<div>
		<oxVideo ref='video' loadGif='/static/loading.gif' :style='boxStyle'></oxVideo>

	</div>
</template>

<script>
	//所有图片支持http开头网络图片
	let w = uni.getSystemInfoSync().windowWidth;
	let h = uni.getSystemInfoSync().windowHeight;
	let music, share, comment, like, avatar, focus, title, userName, musicName, component;
	music = {
		type: 'music',
		x: w - 65,
		y: h - 120,
		w: 80,
		h: 80,
		pic: '',
		code: 16,
		hidden: false
	}; //旋转音乐
	share = {
		type: 'share',
		x: w - 60,
		y: h - 200,
		w: 40,
		h: 40,
		pic: '/static/logo.png',
		code: 17,
		hidden: false,
		num: {
			hidden: false,
			textColor: '#C0FF3E',
			textSize: 12,
			x: w - 60,
			y: h - 160,
			w: 40,
			h: 40
		}
	}; //分享
	comment = {
		type: 'comment',
		x: w - 60,
		y: h - 260,
		w: 40,
		h: 40,
		pic: '/static/logo.png',
		code: 18,
		hidden: false,
		num: {
			hidden: false,
			textColor: '#C0FF3E',
			textSize: 12,
			x: w - 60,
			y: h - 220,
			w: 40,
			h: 40
		}
	}; //评论
	like = {
		type: 'like',
		x: w - 60,
		y: h - 320,
		w: 40,
		h: 40,
		pic: '',
		pic1: '',
		code: 19,
		hidden: false,
		num: {
			hidden: false,
			textColor: '#C0FF3E',
			textSize: 12,
			x: w - 60,
			y: h - 290,
			w: 40,
			h: 40
		}
	}; //红心点赞
	avatar = {
		type: 'avatar',
		x: w - 65,
		y: h - 400,
		w: 50,
		h: 50,
		pic: '',
		radius: 25,
		border: 2,
		borderColor: '#E066FF',
		code: 20,
		hidden: false
	}; //头像
	userName = {
		type: 'userName',
		x: 10,
		y: h - 200,
		w: 150,
		h: 40,
		textSize: 16,
		textColor: '#FFFFFF',
		code: 21,
		hidden: false
	}; //视频简介
	title = {
		type: 'title',
		x: 10,
		y: h - 160,
		w: w - 120,
		h: 80,
		code: 22,
		textSize: 14,
		textColor: '#FFFFFF',
		hidden: false
	}; //用户名
	musicName = {
		type: 'musicName',
		x: 20,
		y: h - 80,
		w: w - 130,
		h: 30,
		textSize: 16,
		textColor: '#FFFFFF',
		code: 23,
		hidden: false
	}; //头像
	focus = {
		type: 'focus',
		x: w - 55,
		y: h - 365,
		w: 30,
		h: 30,
		pic: '',
		code: 25,
		hidden: false
	}; //关注
	component = {
		type: 'component',
		x: 10,
		y: h - 45,
		w: w - 20,
		h: 40,
		radius: 10,
		backgroundColor: '#000000',
		alpha: 0.1,
		border: 0,
		borderColor: '#01000000',
		code: 27,
		hidden: false,
		animation: 0, //隐藏 显示 动画起作用 0正常 1左 2右 3上 4下
		pics: [{
			path: '/static/pan.png',
			x: 10,
			y: 10,
			w: 20,
			h: 20,
			scaleType: 0, //0图片自适应 1 图片撑满 xywh
			radius: 0, //圆角
			code: 271
		}],
		texts: [{
			x: 0,
			y: 0,
			w: 120,
			h: 40,
			text: '说点什么...',
			textSize: 14,
			textColor: '#FFFFFF',
			alignment: 0,
			code: 272
		}]
	}; //自定义控件 评论输入框
	let com = {
		type: 'component',
		x: 20,
		y: h - 450,
		w: 100,
		h: 140,
		radius: 5,
		backgroundColor: '#000000',
		alpha: 0.5,
		border: 0,
		borderColor: '#E066FF',
		code: 666,
		hidden: false,
		animation: 0, //隐藏 显示 动画起作用 0正常 1左 2右 3上 4下
		pics: [{
			path: '/static/product.jpg',
			x: 5,
			y: 20,
			w: 90,
			h: 100,
			scaleType: 0, //0图片自适应 1 图片撑满 xywh
			radius: 0, //圆角
			code: 6661
		}, {
			path: '/static/icon_close.png',
			x: 80,
			y: 0,
			w: 20,
			h: 20,
			scaleType: 0, //0图片自适应 1 图片撑满 xywh
			radius: 0, //圆角
			code: 6662
		}],
		texts: [{
			x: 0,
			y: 0,
			w: 50,
			h: 30,
			text: '旺仔',
			textSize: 14,
			textColor: '#FFFFFF',
			alignment: 0,
			code: 6663
		}, {
			x: 0,
			y: 120,
			w: 50,
			h: 20,
			text: '56.00元',
			textSize: 12,
			textColor: '#FFFFFF',
			alignment: 0,
			code: 6664
		}]
	};
	let styles = [avatar, focus, like, comment, share, music, title, userName, musicName, component];
	//let styles1 = [avatar, focus, like, comment, share, music, title, userName, musicName, component, com];
	let hongbao = {
		type: 'hongbao',
		x: w - 65,
		y: 120,
		w: 50,
		h: 50,
		time: 120, //旋转一周时长
		code: 55, //点击事件返回code
		finishCode: 56, //结束事件返回code
		hidden: false
	};
	let vdata = [{
		"vid": 49,
		"title": "日本政府花160亿日元购岛，方便美军机训练？该岛距离我国...",
		"thumb": "http://p9-dy.byteimg.com/large/tos-cn-p-0015/2e6b13b31a2a40b2aadaade01387584f_1575456802.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200fc40000bnjp049evctvb2f04l90&line=0&ratio=480p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 10,
			"userName": "长江新闻号",
			"avatar": "https://p9-dy.byteimg.com/aweme/100x100/bdf80017d3278f461445.jpeg",
			"isLive": true,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 10,
			"musicName": "长江新闻号@长江新闻号创作的原声",
			"musicIcon": "https://p1-dy.byteimg.com/aweme/100x100/bdf80017d3278f461445.jpeg"
		}
	}, {
		"vid": 45,
		"title": "今生有幸目睹￼二战中打谁都打不过的意大利士兵🇮🇹 #意大利",
		"thumb": "http://p1-dy.byteimg.com/large/tos-cn-p-0015/d6addaee76f3495d840d6dff8d2216e0_1575363173.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200f470000bnj24h87q8i137v8k2t0&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 9,
			"userName": "openg_pongpong",
			"avatar": "https://p1-dy.byteimg.com/obj/2e041000706e748e808a1",
			"isLive": true,
			"isFocus": false,
			"likeNum": 1,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 9,
			"musicName": "好啊油",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/85e6001ea9360b6e1731.jpeg"
		}
	}, {
		"vid": 22,
		"title": "父母的都想把最好的给自己的儿女#父亲 @抖音小助手",
		"thumb": "http://p3-dy.byteimg.com/large/tos-cn-p-0015/818d1fad6be3458e940dcd4b5e3bdaf9_1575374652.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200f120000bnj4u9egncodds6bjgm0&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 7,
			"userName": "南通斑比家纺",
			"avatar": "https://p9-dy.byteimg.com/aweme/100x100/f98e00062c4681f07ecc.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 1,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 7,
			"musicName": "南通斑比家纺@南通斑比家纺创作的原声",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/f98e00062c4681f07ecc.jpeg"
		}
	}, {
		"vid": 40,
		"title": "儿子诈骗19多万挥霍，父亲东拼西凑现金返还受害人@抖音小助手",
		"thumb": "http://p9-dy.byteimg.com/large/tos-cn-p-0015/2d4110d5d01c4bf38b69791bae43c89e_1575435339.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200fc20000bnjjodd8n75ja660q7k0&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 9,
			"userName": "幸福肥东",
			"avatar": "https://p3-dy.byteimg.com/aweme/100x100/1e12d0008a7128b41d591.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 9,
			"musicName": "@幸福肥东创作的原声",
			"musicIcon": "https://p9-dy.byteimg.com/aweme/100x100/1e12d0008a7128b41d591.jpeg"
		}
	}, {
		"vid": 15,
		"title": "这是应该世界上最好听的歌声！@抖音小助手 #边境国门dou平安",
		"thumb": "http://p9-dy.byteimg.com/large/tos-cn-p-0015/11ec23a65dd7452b9d08740038bbfec0_1575378425.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200ffb0000bnj5ro0a2pele7j5h0lg&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 6,
			"userName": "神彩花边",
			"avatar": "https://p9-dy.byteimg.com/aweme/100x100/2e5370002d388bce37cb8.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 6,
			"musicName": "@长虹边境派出所创作的原声",
			"musicIcon": "http://p9-dy.byteimg.com/large/tos-cn-p-0015/11ec23a65dd7452b9d08740038bbfec0_1575378425.jpeg?from=2563711402_large"
		}
	}, {
		"vid": 26,
		"title": "#自驾 #巴基斯坦 没想巴基斯坦还有商场。里面有真功夫！含泪吃汉餐，服务员还给拿了两双一次性的筷子",
		"thumb": "http://p3-dy.byteimg.com/large/tos-cn-p-0015/57bb2936bcb648cba77fc35406b4ff0a_1575460967.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200fc70000bnjpvdgnrm1raagdbapg&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 7,
			"userName": "威廉全世界",
			"avatar": "https://p1-dy.byteimg.com/aweme/100x100/2ddc700046e6aa1611800.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 7,
			"musicName": "@威廉全世界创作的原声",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/2ddc700046e6aa1611800.jpeg"
		}
	}, {
		"vid": 66,
		"title": "可怕，暴徒的“援军”也到了 #香港 #乌克兰 #美国",
		"thumb": "http://p3-dy.byteimg.com/large/tos-cn-p-0015/8f90781e7c1a454b8e65476ab6158b57_1575377986.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200f940000bnj5o7tp06vr26tsohag&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 12,
			"userName": "中国经济网",
			"avatar": "https://p3-dy.byteimg.com/aweme/100x100/db680014ce3a1a96b8ff.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 12,
			"musicName": "@中国经济网创作的原声",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/db680014ce3a1a96b8ff.jpeg"
		}
	}, {
		"vid": 133,
		"title": "你这么好的白菜，又这么有才，谁告诉我司仪去哪了，你想让司仪下岗吗？#抖音小助手 #结婚 #感恩",
		"thumb": "http://p9-dy.byteimg.com/large/tos-cn-p-0015/686c64594e1142ef894c93cddcf39973_1575374384.jpeg?from=2563711402_large",
		"url": "https://aweme.snssdk.com/aweme/v1/play/?video_id=v0200f120000bnj4s5l9688l9evqh8rg&line=0&ratio=540p&watermark=1&media_type=4&vr_type=0&improve_bitrate=0&logo_name=aweme",
		"styles": styles,
		"userInfo": {
			"uid": 49,
			"userName": "🔥森少🔥",
			"avatar": "https://p3-dy.byteimg.com/aweme/100x100/241dc0004e7ed361aba3b.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 19,
			"isLike": false,
			"commentNum": 1,
			"shareNum": 0,
			"musicId": 49,
			"musicName": "@🔥森少🔥创作的原声",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/241dc0004e7ed361aba3b.jpeg"
		}
	}, {
		"vid": 4,
		"title": "@强李6745发呆\r\n\r\n，静静的发呆",
		"thumb": "http://7z2dc9.com1.z0.glb.clouddn.com/apicloud/1a73dd6a90a52b2aad1aafefbf977e4c.png",
		"url": "http://7z2dc9.com1.z0.glb.clouddn.com/apicloud/00b2141bff87cfaa75498f66214aeb9e.mp4",
		"styles": styles,
		"userInfo": {
			"uid": 3,
			"userName": "KF。狂丰",
			"avatar": "https://p1-dy.byteimg.com/aweme/100x100/2ce9300064741169b20cf.jpeg",
			"isLive": false,
			"isFocus": false,
			"likeNum": 0,
			"isLike": false,
			"commentNum": 0,
			"shareNum": 0,
			"musicId": 3,
			"musicName": "@KF。狂丰创作的原声",
			"musicIcon": "https://p3-dy.byteimg.com/aweme/100x100/2ce9300064741169b20cf.jpeg"
		}
	}];
	let test_data = {
		index: 0,
		isLive: false,
		components: [hongbao], // 控件 包括 红包 自定义控件 可选 不随屏滚动控件
		scaleMode: 0, //0 :自动调节 默认  1自适应 2 全屏 有切边 3 全屏 android起作用 
		scrollType: 0, //滑动方向 0 上下滑动  1 左右滑动  默认 上下滑动 注意 开启左右滑动 前关闭左右滑动开关 ios 
		openCache: true, //是否开启缓存
		showBack: true, //返回按钮是否显示事件返回code:0滑动返回code:1android有效
		showShade: true, //头部 底部阴影 是否显示  默认显示
		rightSlide: true, //右滑禁止开关  code 12 监听互动x坐标 为正 浮点型
		leftSlide: true, //左滑禁止开关code 12 监听互动x坐标 为负 浮点型
		freshUp: true, //上拉刷新开关  code 15 
		freshDown: true, //下拉拉刷新开关code 14 
		showDoubleClick: true, //双击红心点赞事件返回code:3
		backgroundColor: '', //视频背景颜色
		backgroundHolder: '/static/background.png', //视频背景颜色
		playBtn: '', //中间播放按钮图片(自定义) 可选 没有则用系统自带
		marginBottom: 55, //进度条距离底部距离
		longClick: false, //11长按事件开关
		data:vdata
	};

	export default {
		data() {
			return {
				boxStyle: {
					'height': 0,
					'width': '750upx',
				}
			}
		},
		onLoad() {
			this.wHeight = uni.getSystemInfoSync().windowHeight;
			this.boxStyle.height = this.wHeight;
		},
		onShow() {},
		onReady() {
			//  0 小屏状态下返回按钮点击 
			//  1 右滑结束(android有效)
			//  2 单击
			//  3 双击
			//  4 滑到最后一个视频返回
			//  5 播放记录返回index滚动到播放记录索引
			//  6 播放 
			//  7 暂停 
			//  8 准备播放返回 
			//  9 网络错误
			//  10 播放完成
			//  11 长按事件 
			//  12 右滑返回坐标与状态
			//  13 左滑返回坐标与状态
			//  14 下拉刷新返回
			//  15 上拉刷新返回
			//  16 progress播放进度
			//  17 缓冲
			//  18 连接失败
			let globalEvent = weex.requireModule('globalEvent');
			let ox = this.$refs.video;
			ox.addCacheDatas(vdata);//提前缓存 封面 短视频
			setTimeout(function() {
				ox.initVideoData(test_data);
			}, 1000);
			globalEvent.addEventListener('actionCallback', function(e) {
					let code = e.code;
					if (code == 4) {
						ox.addDataAfter({data: vdata});
				} else if (code == 5) {
					
				} else if (code == 0) {
					ox.clearCache();//提前清理缓存 封面 短视频
					uni.navigateBack({
						delta: 1,
						animationType: 'pop-out',
						animationDuration: 200
					});
				} else if (code == 6) {
					// ox.hongbaoAction({
					// 	action: 0
					// });
				} else if (code == 7) {
					// ox.hongbaoAction({
					// 	action: 1
					// });
				} else if (code == 14) {
					ox.addDataBefore({data: vdata});
					ox.stopFresh();
				} else if (code == 10) {
					//uni.showToast(e);
				} else if (code == 12) {
					//右滑返回x坐标 state 触屏状态  1 开始触屏 2 移动 3 结束
					let xx = e.x;
					var state = e.state;
					if (xx > w * 0.6 && state == 3) {
						uni.navigateBack({
							delta: 1,
							animationType: 'pop-out',
							animationDuration: 200
						});
					}
				} else if (code == 16) {
					//右滑返回x坐标 state 触屏状态  1 开始触屏 2 移动 3 结束
					//var progress = e.progress;
					//ox.setHBProgress(progress);
				} else if (code == 20) {
					uni.navigateTo({
						url: '/pages/to/to'
					});
				} else if (code == 19) {
					// var vid = e.vid;
					// var userInfo = e.userInfo;
					// userInfo.isLike = e.isLike;
					// ox.updateUserInfo(userInfo);
				} else if (code == 25) {
					// var vid = e.vid;
					// var userInfo = e.userInfo;
					// userInfo.isFocus = e.isFocus;
					// ox.updateUserInfo(userInfo);
				} else if (code == 3) {
					// var vid = e.vid;
					// var userInfo = e.userInfo;
					// userInfo.isLike = true;
					// userInfo.productId = 'ddddd';
					// ox.updateUserInfo(userInfo);
				} else if (code == 27) {
					//uni.showToast(e);
				}
			})

	},
	methods: {
		updateUserInfo: function() {
			var ox = this.$refs.video;
			//ox.updateUserInfo({userInfo});
			//更新用户信息
		},
		updateComponent: function() {
			var ox = this.$refs.video;
			//ox.updateComponent({component});
			//更新组件 红包 自定义 不随屏滚动控件
		},
		addComponent: function() {
			var ox = this.$refs.video;
			//ox.addComponent({component});
			//添加自定义组件 自定义 不随屏滚动控件
		},
		updateStyles: function() {
			var ox = this.$refs.video;
			//ox.updateStyles([style]);
			//动态更新控件 随屏滚动的控件
		},
		addStyle: function() {
			var ox = this.$refs.video;
			//ox.addStyle({component});
			//动态添加控件 随屏滚动的控件
		},

		addDataAfter: function() {
			var ox = this.$refs.video;
			//ox.addDataAfter({data:[]});
			//追加数据 data内为视频数据列表
		},
		addDataBefore: function() {
			//ox.addDataBefore({data:[]});
			//下拉刷新更新一组数据 data内为视频数据列表
		},
		clearCache: function() {
			var ox = this.$refs.video;
			ox.clearCache();
			//清理缓存
		},
		next: function() {
			var ox = this.$refs.video;
			ox.next();
			//播放下一条记录
		},
		prev: function() {
			var ox = this.$refs.video;
			ox.prev();
			//播放上一条记录
		},
		playIndex: function() {
			var ox = this.$refs.video;
			ox.playIndex(2);
			//播放索引记录
		},
		start: function() {
			var ox = this.$refs.video;
			ox.start();
			//开始播放
		},
		pause: function() {
			var ox = this.$refs.video;
			ox.pause();
			//暂停播放
		},
		replay: function() {
			var ox = this.$refs.video;
			ox.replay();
			//循环播放
		},
		remove: function() {
			var ox = this.$refs.video;
			ox.remove();
			//去除播放器
		},
		hidePlay: function() {
			var ox = this.$refs.video;
			ox.hidePlay();
			//隐藏播放器
		},
		showPlay: function() {
			var ox = this.$refs.video;
			ox.showPlay();
			//显示播放器
		},
		hongbaoAction: function() {
			var ox = this.$refs.video;
			ox.hongbaoAction({
				action: 0
			});
			//控制红包 //0 开始红包进度条 1停止 2显示 3隐藏
		},
		setHBProgress: function() {
			var ox = this.$refs.video;
			ox.setHBProgress(20);
			//设置红包进度  1-100

		},
		getDuration: function() {
			var ox = this.$refs.video;
			ox.duration(result => {
				let duration = result.duration;
			});
			//获取视频时长 毫秒

		},
		getScreenShot: function() {
			var ox = this.$refs.video;
			ox.screenShot(result => {
				let base64 = result.base64;
			});
			//截图 返回base64

		},
		getInfo: function() {
			var ox = this.$refs.video;
			ox.getInfo(result => {
				let duration = result.duration;
				let position = result.position;
				let item = result.item;
			});
			//获取当前视频信息  返回 duration position item

		},
		setOptionValue: function() {
			var ox = this.$refs.video;
			ox.setOptionValue({
				value: '',
				key: '',
				category: 1
			});
			//ijk设置 option category 1 FormatOption 2 CodecOption 3 SwsOption 4 PlayerOption
		},
		setOptionIntValue: function() {
			var ox = this.$refs.video;
			ox.setOptionIntValue({
				value: 0,
				key: '',
				category: 1
			});
			//ijk设置 option category 1 FormatOption 2 CodecOption 3 SwsOption 4 PlayerOption
		},
		setScreenScaleType: function() {
			var ox = this.$refs.video;
			ox.setScreenScaleType(1);
			//设置视频画面 适应 1 2 3
		},
		showLiveControlls: function() {
			var ox = this.$refs.video;
			ox.showLiveControlls();
			//显示直播控件
		},
		hideLiveControlls: function() {
			var ox = this.$refs.video;
			ox.hideLiveControlls();
			//隐藏直播控件
		}
	}
	};
</script>
<style>

</style>
