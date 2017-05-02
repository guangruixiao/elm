<template>
    <div class="sellerheader">
      <div class="content-wrapper">
        <img class="avatar" width="64" height="64" v-bind:src=sellerMessage.avatar alt="">
        <div class="content">
          <div class="title">
            <span class="brand"></span>
            <span class="name">{{sellerMessage.name}}</span>
          </div>
          <div class="description">{{sellerMessage.description}}/{{sellerMessage.deliveryTime}}分钟送达</div>
          <div class="supports" v-if=sellerMessage.supports>
            <icon class="supports-icon" v-bind:size="1" v-bind:type="(sellerMessage.supports[0].type)"></icon>
            <span class="supports-text">{{sellerMessage.supports[0].description}}</span>
          <div class="supports-click" v-on:click="sellerlistshow">
            <span class="supports-count">{{sellerMessage.supports.length}}个</span>
            <i class="icon-keyboard_arrow_right"></i>
          </div>
          </div>
        </div>
      </div>
      <div class="bulletin"  v-on:click="sellerlistshow" >
        <span class="bulletin-icon"></span>
        <span class="bulletin-text"> {{sellerMessage.bulletin}}</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
      <div class="background">
        <img v-bind:src=sellerMessage.avatar width="100%" height="100%">
      </div>
      <transition name="fade">
        <div class="detail" v-if="sellerdetail" >
          <div class="detail-wrapper clearfix">
            <div class="detail-main">
              <div class="detail-header">
                <h1 class="detail-name">{{sellerMessage.name}}</h1>
                <star class="detail-star" v-bind:size="48"  v-bind:score="(sellerMessage.score)"></star>
              </div>
              <div class="detail-title">
                <div class="title-line"></div>
                <div class="title-name">优惠信息</div>
                <div class="title-line"></div>
              </div>
              <div class="detail-supports" v-for="item in (sellerMessage.supports)">
                <icon class="detail-icon" v-bind:size="2" v-bind:type="(item.type)"></icon>
                <span class="detail-description">{{item.description}}</span>
              </div>
              <div class="detail-title">
                <div class="title-line"></div>
                <div class="title-name">商家公告</div>
                <div class="title-line"></div>
              </div>
              <div class="detail-bulletin">
                <p>{{sellerMessage.bulletin}}</p>
              </div>
            </div>
          </div>
          <div class="detail-close" v-on:click="sellerlistshow">
            <i class="icon-close"></i>
          </div>
        </div>
      </transition>

    </div>
</template>
<script>
import star from '../star/star'
import icon from '../icon/icon'

export default {
  props:["sellerMessage"],
  data() {
    return {
      sellerdetail: false
    };
  },

  methods:{
    sellerlistshow:function(){
      if(this.sellerdetail==false){
        this.sellerdetail=true;
      }else{
        this.sellerdetail=false;
      }
    }
  },
  components: {
    star,
    icon
  }
}
</script>
<style lang="scss" scoped>
 @import '../../common/scss/_mixin.scss';
  .sellerheader{
    position: relative;
    overflow:hidden;
    color:white;
    background-color:rgba(7,17,27,0.5);
    blur:10px;
    .content-wrapper{
      position:relative;
      width:100%;
      height:106px;
      .avatar{
        margin-left:24px;
        margin-top:24px;
        border-radious:2px;
      }
      .content{
        display: inline-block;
        margin-left: 16px;
        .title{
          .brand{
            display:inline-block;
            vertical-align: top;
            width:30px;
            height:18px;
            @include bg-image("brand");
            background-size: 30px 18px;
            background-repeat: no-repeat;
          }
          .name{
            margin-left: 6px;
            font-size: 16px;
            line-height: 18px;
            font-weight: bold;
          }
        }
        .description{
          margin-top:8px;
          line-height: 12px;
          font-size: 12px;
        }
        .supports{
          font-size: 0;
          margin-top:10px;
          .supports-icon{
            display:inline-block;
            vertical-align:bottom;
            width: 12px;
            height: 12px;
          }
          .supports-text{
            display:inline-block;
            vertical-align:bottom;
            margin-left:4px;
            line-height: 12px;
            font-size: 10px;
          }
        }
      }
      .supports-click{
        position: absolute;
        right: 12px;
        bottom: 14px;
        padding: 0 8px;
        height: 24px;
        line-height: 24px;
        border-radius: 14px;
        background: rgba(0, 0, 0, 0.2);
        text-align: center;
        .supports-count{
          font-size: 10px;
        }
        .icon-keyboard_arrow_right{
          margin-left:4px;
          font-size: 10px;
        }
      }
    }
    .bulletin{
      position: relative;
      height:28px;
      padding: 0 24px 0 12px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      background-color:rgba(7,17,27,0.2);
      .bulletin-icon{
        display:inline-block;
        vertical-align: middle;
        width:22px;
        height:12px;
        @include bg-image("bulletin");
            background-size: 22px 12px;
            background-repeat: no-repeat;
      }
      .bulletin-text{
        margin: 0 4px;
        line-height:28px;
        font-size:10px;
        color:rgb(255,255,255);
      }
      .icon-keyboard_arrow_right{
        position: absolute;
        font-size: 10px;
        right: 8px;
        top: 8px;
      }
    }
    .background{
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      filter: blur(10px);
    }
    .detail{
      &.fade-enter-active, &.fade-leave-active {
        transition: opacity .5s;
      }
      &.fade-enter, &.fade-leave-active {
        opacity: 0;
      }
      position:fixed;
      left:0;
      top:0;
      z-index: 100;
      width:100%;
      height:100%;
      overflow:auto;
      background-color:rgba(7,17,27,0.8);
      .detail-wrapper{
        width: 100%;
        min-height: 100%;
        .detail-main{
          margin:64px auto 0 auto;
          padding-bottom:64px;
          width:80%;
          .detail-header{
            text-align:center;
            .detail-name{
              display:inline-block;
              padding:0 auto;
              font-size:16px;
              line-height:16px;
              font-weight:700;
              color:rgb(255,255,255)
            }
            .detail-star{
              margin-top:16px;
              height:24px;
            }
          }
          .detail-title{
            display:flex;
            margin:30px auto 24px auto;
            .title-line{
              flex:1;
              position:relative;
              top:-6px;
              border-bottom: 1px solid rgba(255,255,255,0.2)
            }
            .title-name{
              padding:0 12px;
              font-size:14px;
              line-height:14px;
              font-weight:700;
              color:rgb(255,255,255)
            }
          }
          .detail-supports{
            margin-top:24px;
            margin-left:12px;
            margin-right:12px;
            .detail-icon{
              margin-bottom:12px;
              vertical-align: top;
              &:last-child{
              margin-bottom: 0;
              }
            }
            .detail-description{
              display:inline-block;
              margin-left:6px;
              font-size:12px;
              line-height:12px;
              font-weight:200;
              color:rgb(255,255,255);
            }
          }
          .detail-bulletin{
            margin-top:24px;
            margin-left:12px;
            margin-right:12px;
            font-size:12px;
            line-height:24px;
            font-weight:200;
            color:rgb(255,255,255);

          }
        }
      }
      .detail-close{
        position: relative;
        width: 32px;
        height: 32px;
        margin: -64px auto 0 auto;
        clear: both;
        font-size: 32px;
      }
    }
  }
</style>
