<template>
  <view>
    <image src="/static/images/beijing.jpg" mode="" class="bg"></image>
    <view class="body">
     
      <view class="input-user">
        <image src="/static/images/user.png" mode=""></image>
        <input type="text" placeholder="用户名/手机号" />
      </view>

      <view class="input-passwd">
        <image src="/static/images/passwd.png" mode=""></image>
        <input :type="hidePwd?'password':'text'" placeholder="密码" />
        <view  hover-class="btn-active" @click="hidePwd = !hidePwd">
        <image  :src="`/static/images/${hidePwd?'bkj':'kj'}.png`" mode=""></image>
        </view>
      </view>

      <view hover-class="btn-active" class="btn-login">
        登&nbsp;&nbsp;&nbsp;&nbsp;录
      </view>
      
      <view class="btn-wj"> 
        <view hover-class="btn-active">忘记密码?</view>
        <view  hover-class="btn-active">立即注册</view>
      </view>
    </view>
    
    <view class="footer">
      <view>
        <view style="height: 1px; width: 200rpx; background-color: white;"></view>
        <view style="color: white; font-size: 0.9em; margin: 0 10rpx;">第三方直接登录</view>
        <view style="height: 1px; width: 200rpx;background-color: white;"></view>
      </view>
      <view>
        <view hover-class="btn-active">
          <image src="/static/images/qq.png" mode=""></image>
        </view>
        <view hover-class="btn-active">
          <image src="/static/images/wx.png" mode=""></image>
        </view>
        <view hover-class="btn-active">
          <image src="/static/images/wb.png" mode=""></image>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      // 密码的可见性
      hidePwd:true
    };
  },
  methods: {}
};
</script>

<style lang="scss">
.bg {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  filter: blur(0px);
  // z轴层级: 如果不设置 会遮盖层级低的元素
  z-index: -1;
}

.body {
  // background-color: rgba(0, 0, 0, 0.5);
  width: 600rpx;
  padding-top: 150rpx;
  margin: 0 auto;
  display: flex;
  flex-direction: column;

  > image {
    width: 360rpx;
    height: 100rpx;
    background-color: white;
    border-radius: 10rpx;
    align-self: center;
  }

  > .input-user {
    background-color: white;
    padding: 20rpx;
    border-radius: 10rpx;
    display: flex;
    align-items: center;
    margin-top: 80rpx;

    > image {
      width: 40rpx;
      height: 40rpx;
      margin-right: 20rpx;
    }
  }

  > .input-passwd {
    background-color: white;
    padding: 20rpx;
    border-radius: 10rpx;
    display: flex;
    align-items: center;
    margin-top: 30rpx;

    > image:first-of-type {
      width: 40rpx;
      height: 40rpx;
      margin-right: 20rpx;
    }

    >view{
      margin-left: auto;
      margin-right: 20rpx;
      > image:last-of-type {
        width: 40rpx;
        height: 40rpx;
      }
    }
  }
}

.btn-login {
	opacity: 1;
  background-color: #43a9a1;
  color: white; 
  padding: 15rpx ;
  text-align: center;
  border-radius: 10rpx;
  margin-top: 40rpx;
}

// 按钮点击时的效果, 和 view 的 hover-class 绑定
.btn-active {
  opacity: 0.7;
}

.btn-wj{
  margin-top: 30rpx;
  display: flex;
  justify-content: space-between;
  color: rgba(255,255,255,0.7);
  font-size: 0.8em;
  padding: 0 20rpx;
  
  view{
    text-decoration: underline;
  }
}

.footer{
  position: fixed;
  bottom: 80px;
  // background-color: green;
  width: 100%;
  
  
  >view:first-of-type{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  >view:last-of-type{
    display:flex;
    justify-content: center;
    margin-top: 50rpx;
    
    image{
      width: 100rpx;
      height: 100rpx;
    }
    
    >view:nth-of-type(2){
      margin: 0 60rpx;
    }
  }
}
</style>
