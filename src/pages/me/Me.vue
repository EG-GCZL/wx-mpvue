<template>
  <div class="container">
    <div class="userinfo" >
      <img :src ='userinfo.avatarUrl' alt="" />
      <p>{{userinfo.nickName}}</p>
    </div>
    <YearProgress></YearProgress>
    <button class="btn">添加图书</button>
  <div id="persons">
    <button open-type="getUserInfo"  @getuserinfo="doLogin">用户登陆</button>
    </div>
    </div>
</template>

<script>
    import qcloud from 'wafer2-client-sdk'
    import {get,showSuccess} from "../../util";
    import config from '../../config'
    export default {
        data(){
          return {
              userinfo:{}
          }
        },
        create(){
            // this.login()
        },
        methods:{
            doLogin: function (e) {
                let user = this.userInfo
                if(!user){
                    qcloud.setLoginUrl(config.loginUrl)
                    qcloud.login({
                        success: function (userinfo) {
                            showSuccess('登陆成功')
                            this.userinfo = userinfo
                            console.log(this.userinfo.nickName)
                            wx.setStorageSync('userinfo',userinfo)
                            console.log('登录成功', userinfo)
                        },
                        fail: function (err) {
                            console.log('登录失败', err)
                        }
                    })
                }

            }
            // login (e) {
            //     console.log('触发')
            //     qcloud.setLoginUrl(config.loginUrl)
            //     const session = qcloud.Session.get()
            //     console.log(session)
            //     if (session) {
            //         // 第二次登录
            //         // 或者本地已经有登录态
            //         // 可使用本函数更新登录态
            //         qcloud.loginWithCode({
            //             success: res => {
            //                 this.setData({ userInfo: res, logged: true })
            //                 console.log(res)
            //             },
            //             fail: err => {
            //                 console.error('222', err)
            //             }
            //         })
            //     } else {
            //         // 首次登录
            //         qcloud.login({
            //             success: res => {
            //                 console.log(res)
            //                 this.setData({ userInfo: res, logged: true })
            //             },
            //             fail: err => {
            //                 console.log(err)
            //             }
            //         })
            //     }
            // },
            // doLogin (e) {
            //     console.log('111', e.mp.detail.userInfo)
            // }
        }


    }

</script>
<style lang="scss">
  .container {
    padding:0 30rpx;
    .userinfo {
      margin-top:100rpx;
      img {
        width:200rpx;
        height: 200rpx;
      }
    }
  }
</style>
