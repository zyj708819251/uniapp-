<template>
    <view>
        <u-grid :border="true">
            <u-grid-item v-for="(baseListItem, baseListIndex) in baseList" :key="baseListIndex" @click="click(baseListItem)">
                <u-icon :customStyle="{ paddingTop: 20 + 'rpx' }" :name="baseListItem.name" :size="22"></u-icon>
                <text class="grid-text">{{ baseListItem.title }}</text>
            </u-grid-item>
        </u-grid>
    </view>
</template>

<script>
export default {
    data() {
        return {
            baseList: [
                {
                    name: "photo",
                    title: "二维码",
                    path: "/pages/ewm/index"
                },
                {
                    name: "lock",
                    title: "通讯录",
                    path: "/pages/txl/index"
                },
                {
                    name: "star",
                    title: "扫码",
                    path: "/pages/sm/index"
                },
                {
                    name: "hourglass",
                    title: "一键登录",
                    path: "/pages/dl/index"
                },
                {
                    name: "hourglass",
                    title: "语音识别",
                    path: "/pages/voice/index"
                },
                {
                    name: "hourglass",
                    title: "外链",
                    path: "/pages/webview/index"
                },{
                    name: "hourglass",
                    title: "定位",
                    path: "/pages/dw/index"
                }
            ]
        };
    },
    onNavigationBarButtonTap(e) {
    			console.log(e)
    			if(e.text == 'add'){
                    console.log('添加');
    				
    			}else if(e.text == 'del'){
                    console.log('删除');
    				
    			}
    		},
    methods: {
        click(item) {
            uni.navigateTo({
                //保留当前页面，跳转到应用内的某个页面
                url: item.path
            });
        }
    }
};
</script>

<style lang="scss"></style>
