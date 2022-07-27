<template>
  <div class="home">
    <van-nav-bar title="发布问题" left-text="取消" right-text="发布" @click-left="onClickLeft" @click-right="onClickRight" />
    <div class="title"><span class="start">*</span><input type="text" v-model="title" placeholder="请输入问题标题"></div>
    <van-field v-model="message" rows="1" autosize type="textarea" placeholder="添加问题描述" />
    <van-uploader v-model="fileList" multiple :max-count="1" upload-icon="plus" />

    <div class="add-skill">
      <img src="@/assets/标签.png" alt="">
      <div class="skill">添加备注<span class="start">*</span></div>
    </div>
    <input class="remarks" v-model="remark" type='textarea' placeholder="添加备注会获得更多关注，问题更容易得到解答"/>
    <div class="hide">
      <div class="left">
        <img src="@/assets/隐藏.png" alt="">
        <div class="skill">匿名发布</div>
      </div>
      <van-switch v-model="checked" active-color="#32CD32" inactive-color="#dcdee0" />
    </div>

    <div class="btn">
      <div :class="title!=''&&message!=''?'button':'button1'" @click="releaseClick">发布</div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import { NavBar, Toast, Uploader, Field, Switch } from 'vant'
Vue.use(NavBar)
Vue.use(Field)
Vue.use(Uploader)
Vue.use(Switch)
export default {
  name: 'HomeView',
  data () {
    return {
      title:'',
      message: '',
      checked: true,
      fileList: [],
      remark:''
    }
  },
  methods: {
    onClickLeft () {
      Toast('返回')
    },
    onClickRight () {
      Toast('提交成功')
    },
    afterRead (file) {
      // 此时可以自行将文件上传至服务器1232123231313
      console.log(file);
    },
    // 发布
     releaseClick(){
      if(this.title!=''&&this.message!=''){
        console.log("发布表单:","1.问题标题：",this.title,',2.问题描述：',this.message,'3.添加备注：',this.remark!=''?this.remark:'空',',4.上传文件：',this.fileList.length>0?this.fileList[0].content:'未上传文件')
      }else{
        if(this.title==''){
          this.$toast('请填写问题标题！！');
        }
        if(this.message==''){
          this.$toast('请填写问题描述！！');
        }
      }
   }
  },
}
</script>
<style lang="less" scoped>
.home {
  /deep/ .van-nav-bar__content {
    background-color: #3366cc;
    .van-nav-bar__text {
      color: #fff;
    }
    .van-nav-bar__title {
      color: #fff;
      font-weight: 600;
    }
  }
  .title {
    margin: 8px 15px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid #ccc;
    .start {
      color: red;
      font-size: 32px;
    }
    input {
      border: none;
      font-weight: 600;
    }
  }
  /deep/.van-field__body {
    padding-left: 10px;
  }
  /deep/ .van-uploader__wrapper {
    margin-top: 30px;
    margin-left: 15px;
  }
  .add-skill {
    display: flex;
    align-items: center;
    border-top: 1px solid #ccc;
    padding: 8px 15px;
    img {
      width: 20px;
      height: 20px;
      margin-right: 5px;
    }
    .skill {
      .start {
        color: red;
      }
    }
  }
  .remarks {
    // color: #ccc;
    font-size: 14px;
    width: 80%;
    margin: 0 15px 12px;
    padding-left: 20px;
    border: none;
  }

  .hide {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-top: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    padding: 8px 15px;
    .left {
      display: flex;
      img {
        width: 20px;
        height: 20px;
        margin-right: 5px;
      }
    }
  }

  .btn {
    position: fixed;
    left: 0;
    bottom: 0;
    right: 0;
    border-top: 1px solid #ccc;
    display: flex;
    justify-content: flex-end;
    .button {
      width: 70px;
      height: 25px;
      color: #fff;
      background-color: #FF8200;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 8px 0;
      margin-right: 15px;
    }
    .button1 {
      width: 70px;
      height: 25px;
      color: #fff;
      background-color: #FED9B2;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 8px 0;
      margin-right: 15px;
    }
  }
}
</style>