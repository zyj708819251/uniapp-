<template>  
    <view>  
        <button type="primary" @tap="getContacts">获取联系人</button>
 
        <view class="item" v-for="(item,index) in contactsList" :key="index">  
            <view>{{item.displayName}}</view>  
            <view v-for="(subItem,subIndex) in item.phoneNumbers" :key="subIndex">  
                <view>{{subItem.value}}</view>  
            </view>  
        </view>
 
    </view>  
</template>  
 
<script>  
    var Contacts  
    export default {  
        data() {  
            return {  
                contactsList: []  
            }  
        },  
        onShow() {  
            uni.setNavigationBarTitle({  
                title: '通讯录'  
            });  
        },  
        methods: {  
            getContacts: function() {  
                var _this = this; 
                // 获取通讯录对象  
                plus.contacts.getAddressBook( plus.contacts.ADDRESSBOOK_PHONE, function( addressbook ) {  
                    uni.showToast({  
                        title: '获取通讯录对象成功',  
                        duration: 2000  
                    })  
                    console.log('获取通讯录对象成功')  
                    console.log(addressbook)  
                    // 查找联系人  
                    addressbook.find(["displayName","phoneNumbers"],function(contacts){  
                        uni.showToast({  
                            title: '获取联系人成功',  
                            duration: 2000  
                        })  
                        console.log('获取联系人成功')  
                        console.log(JSON.stringify(contacts))  
                        _this.contactsList= contacts;
                    }, function () {  
                        uni.showToast({  
                            title: '获取联系人失败',  
                            duration: 2000  
                        })  
                    },{multiple:true});  
                }, function ( e ) {  
                    uni.showToast({  
                        title: '获取通讯录对象失败:' + e.message,  
                        duration: 2000  
                    })  
                });  
            }  
        }  
    }  
</script>  
 
<style>  
 .item{
     display: flex;
     justify-content: space-between;
     padding: 10px 20px;
     border-bottom: 1px solid #CCC;
 }
</style>