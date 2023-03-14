<template>
    <view class="content">
        <button @click="startLuyin" class="recordingStyle">按住开始说话</button>
        <view>识别的结果 : {{ searchText }}</view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            speechEngine: "baidu",
            searchText: "",
            islongPress: false
        };
    },

    methods: {
        startLuyin() {
            console.log("语音输入");
            let _this = this;
            let options = {};
            options.engine = _this.speechEngine;
            options.punctuation = false; // 是否需要标点符号
            options.timeout = 20 * 1000; //超时时间
            plus.speech.startRecognize(
                options,
                s => {
                    console.log(s); //识别的结果
                    _this.searchText = s;
                    plus.speech.stopRecognize();
                    if(_this.searchText.includes('百度')){
                        // uni.showToast({
                        //     //显示对话框
                        //     title: "百度成功",
                        //     icon: "none",
                        //     duration: 5000
                        // });
                        console.log(222222222222);
                      setTimeout(()=>{
                          
                        uni.navigateTo({
                            //保留当前页面，跳转到应用内的某个页面
                            url: '/pages/webview/index?url=http://www.baidu.com'
                        });
                      })
                    }
                },
                s => {
                    console.log(s);
                    uni.showToast({
                        //显示对话框
                        title: "识别失败",
                        icon: "none",
                        duration: 1000
                    });
               }
            );
        },
        
    }
};
</script>

<style>
.content {
    padding: 20px;
}

.recordingStyle {
    border-radius: 20px;
    text-align: center;
    color: #fff;
    font-size: 15px;
    background-color: #409eff;
    margin-bottom: 15px;
}
</style>
