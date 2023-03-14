<template>
    <view>
        <button type="primary" @tap="sm">扫码</button>
        <view>识别的结果 : {{ info }}</view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            info: ""
        };
    },
    methods: {
        sm() {
            uni.scanCode({
                success: res => {
                    var a = res.result;
                    this.info = a;
                    console.log(a);
                },
                fail: err => {
                    uni.getSetting({
                        success: res => {
                            let authStatus = res.authSetting["scope.camera"];
                            if (!authStatus) {
                                uni.showModal({
                                    title: "授权失败",
              		                    content: "需要使用您的相机，请在设置界面打开相关权限",
               									            success: res => {
                                        if (res.confirm) {
                                            uni.openSetting();
                                        }
                                    }
                                });
                            }
                        }
                    });
                }
            });
        }
    }
};
</script>

<style lang="scss"></style>
