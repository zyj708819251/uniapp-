<template>
    <view class="pages">
        <view class="father_view">
            <view class="son_view">
                <view class="title-bg">需要转换的文本：</view>
                <textarea class="textarea-bg" v-model="text1" @blur="inputText" placeholder="请在这里输入" />
            </view>
        </view>
        <button @click="btn">生成二维码</button>
        <!-- 
        

        <button @click="saveImage">下载二维码</button>
        <button @click="share">分享二维码</button>
         -->

        <u-popup mode="center" :show="show" @close="show = false" :closeable="true">
            <view>
                <view>二维码</view>
                <view class="qr-box"><canvas canvas-id="qrcode" v-show="qrShow" style="width: 300px;height: 300px;" /></view>
                <button @click="share">分享二维码</button>
            </view>
        </u-popup>
    </view>
</template>

<script>
import uQRCode from "@/common/uqrcode.js"; //引入uqrcode.js
export default {
    data() {
        return {
            qrShow: false,
            text1: "",
            show: false
        };
    },
    methods: {
        share() {
            uni.showLoading({ title: "正在生成图片..." });
            uni.canvasToTempFilePath({
                x: 0,
                y: 0,
                width: 300,
                height: 300,
                destWidth: 300,
                destHeight: 300,
                canvasId: "qrcode",
                complete: res => {
                    uni.saveImageToPhotosAlbum({
                        filePath: res.tempFilePath,
                        success: data => {
                            uni.shareWithSystem({
                                type: "image",
                                imageUrl: res.tempFilePath,
                                success: function() {},
                                fail: function() {
                                    uni.showToast({ title: "分享失败" });
                                }
                            });
                        },
                        fail: err => {
                            console.log(err);
                        },
                        complete: () => {
                            uni.hideLoading();
                        }
                    });
                }
            });
        },
        // 保存图片
        saveImage: function() {
            uni.showLoading({ title: "正在生成图片..." });
            uni.canvasToTempFilePath({
                x: 0,
                y: 0,
                width: 300,
                height: 300,
                destWidth: 300,
                destHeight: 300,
                canvasId: "qrcode",
                complete: res => {
                    console.log(res.tempFilePath);
                    uni.saveImageToPhotosAlbum({
                        filePath: res.tempFilePath,
                        success: data => {
                            uni.showToast({
                                title: "已保存至手机相册",
                                icon: "none"
                            });
                            uni.hideLoading();
                        },
                        fail: err => {
                            console.log(err);
                        },
                        complete: () => {
                            uni.hideLoading();
                        }
                    });
                }
            });
        },
        //*获取文本框内容*//
        inputText: function(e) {
            this.text1 = e.detail.value;
        },

        //*按钮*//
        btn: function() {
            if (this.text1 == "") {
                console.log("aaaaaaaa");
                uni.showToast({
                    //显示对话框
                    title: "请输入文本",
                    icon: "none",
                    duration: 1000
                });
            } else {
                var text = "";
                if (this.text1 == "百度") {
                    text = "http://www.baidu.com";
                } else {
                    text = this.text1;
                }
                this.qrFun(text); //调用二维码方法
            }
        },

        //**生成二维码**//
        qrFun: function(text) {
            this.show = true;
            this.qrShow = true;
            uQRCode.make({
                canvasId: "qrcode",
                componentInstance: this,
                text: text,
                size: 300,
                margin: 0,
                backgroundColor: "#ffffff",
                foregroundColor: "#000000",
                fileType: "jpg",
                errorCorrectLevel: uQRCode.errorCorrectLevel.H,
                success: res => {
                    let ctx = uni.createCanvasContext("qrcode");

                    // ctx.drawImage(res, 0, 0, 300, 300);

                    ctx.font = "20px Georgia";
                    ctx.fillStyle = "#ff0000";
                    ctx.textAlign = "center";
                    ctx.textBaseline = "middle";
                    ctx.fillText("Hello World!", 150, 150);
                    
                    ctx.draw(true)
                     
                     
                      // ctx.fillStyle = "#ff0000"; // 设置填充颜色为白色
                               // ctx.strokeStyle = "#000000"; // 设置描边颜色为黑色
                               // ctx.lineWidth = 2; // 设置描边宽度为2个像素
                               // ctx.font = "bold 20px Arial"; // 设置字体和大小
                               // ctx.textAlign = "center";
                               // ctx.textBaseline = "middle";
                               // ctx.strokeText(text, 50, 50); // 先描边
                               // ctx.fillText(text, 50, 50); // 再填充
                     
                     
                     
                }
            });
        }
    }
};
</script>

<style>
.pages {
}

/* 多行文本 */
textarea {
    width: 98%;
    height: 250rpx;
}

.textarea-bg {
    width: 94%;
    border-style: solid;
    border-color: #ff007f;
    font-size: 32rpx;
}

button {
    width: 80%;
    background-color: #ffaa00;
}

.qr-box {
    height: 300px;
}
</style>
