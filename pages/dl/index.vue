<template>
    <view>
        <button type="primary" @tap="weixinLogin">微信登录</button>
        <button type="primary" @tap="qqLogin">QQ登录</button>
        <view>昵称 : {{ nickname }}</view>
        <view>
            头像 :
            <image class="avatar" :src="img"></image>
        </view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            nickname: null,
            img: null
        };
    },
    methods: {
        weixinLogin() {
            uni.login({
              provider: 'weixin',
              success: (loginRes) => {
                console.log(loginRes);
                // 获取用户信息
                uni.getUserInfo({
                  provider: 'weixin',
                  success:  (infoRes) =>{
                      this.nickname=infoRes.userInfo.nickName;
                      this.img=infoRes.userInfo.avatarUrl;
                    console.log('用户昵称为：' + JSON.stringify(infoRes));
                  }
                });
              }
            });
        },
        qqLogin(){
            uni.login({
                provider:'qq',
                success: (loginRes) => {
                    console.log(loginRes);
                    uni.getUserInfo({
                        provider:'qq', 
                        success: (infoRes) => {
                            console.log("successreq"+JSON.stringify(successreq))
                        }
                    })
                }
            })
        }


    }
};
</script>

<style lang="scss">
.avatar {
    width: 100rpx;
    height: 100rpx;
    border-radius: 50%;
}
</style>
