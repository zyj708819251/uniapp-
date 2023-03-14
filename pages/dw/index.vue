<template>
    <view class="">
        <button type="primary" @tap="getLocation">获取位置</button>
        <view class="">经度：{{ jd }}</view>
        <view class="">纬度：{{ wd }}</view>

        ===============================
        <view class="">经度1：{{ jd1 }}</view>
        <view class="">纬度1：{{ wd1 }}</view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            show: false,
            jd: null,
            wd: null,
            jd1: null,
            wd1: null
        };
    },
    mounted() {},
    methods: {
        getLocation() {
            uni.getLocation({
                type: "wgs84",
                geocode: true,
                success: res => {
                    this.jd = res.longitude;
                    this.wd = res.latitude;
                    console.log(res);
                },
                fail: res => {
                    console.log(res);
                }
            });

            plus.geolocation.getCurrentPosition(
                res => {
                    this.jd1 = res.coords.longitude;
                    this.wd1 = res.coords.latitude;
                },
                error => {
                    uni.showToast({
                        title: error.message,
                        duration: 3000,
                        icon: "icon"
                    });
                }
            );
        }
    }
};
</script>

<style></style>
