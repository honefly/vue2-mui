<style lang="less" rel="stylesheet/less">
  @import "public/common.css";
  // @import "public/mui.css";
  @import "public/app.css";

  .mui-bar-tab .mui-tab-item .mui-icon .mui-badge {
    height: 10px;
  }

  .mui-bar-tab .mui-tab-item.mui-active {
    color: #C37573;
  }

  .loadAppShadeLogo1::before {
    font-family: Muiicons;
    content: "\e811";
    font-size: 50px;
    color: #f58c26;
    position: absolute;
    bottom: 0px;
    bottom: 0px;
    margin-left: -25px;
  }

  .loadAppShadeLogo1 {
    position: relative;
    height: 40%;
    text-align: center;
  }

  .mui-content {
    margin-top: 44px;
  }
  .router-fade-enter-active, .router-fade-leave-active {
	  	transition: opacity .3s;
	}
	.router-fade-enter, .router-fade-leave-active {
	  	opacity: 0;
  }
  

    .router-slid-enter-active, .router-slid-leave-active {
        transition: all .4s;
    }
    .router-slid-enter, .router-slid-leave-active {
        transform: translate3d(2rem, 0, 0);
        opacity: 0;
    }


  .vux-pop-out-enter-active,
  .vux-pop-out-leave-active,
  .vux-pop-in-enter-active,
  .vux-pop-in-leave-active {
    will-change: transform;
    transition: all 300ms;
    height: 100%;
    top: 0;
    position: absolute;
    backface-visibility: hidden;
    perspective: 1000;
  }
  .vux-pop-out-enter {
    opacity: 0;
    transform: translate3d(-100%, 0, 0);
  }
  .vux-pop-out-leave-active {
    opacity: 0;
    transform: translate3d(100%, 0, 0);
  }
  .vux-pop-in-enter {
    opacity: 0;
    transform: translate3d(100%, 0, 0);
  }
  .vux-pop-in-leave-active {
    opacity: 0;
    transform: translate3d(-100%, 0, 0);
  }
</style>

<template>
  <div>

    <!-- <mui-header :title="title">
      <mui-header-btn v-for="(btn, index) in currentHeader.btns"
                      :position="btn.pos"
                      :icon="btn.icon"
                      :label="btn.text"
                      :show="btn.show"
                      :key="index"
      >
      </mui-header-btn>
    </mui-header> -->


    <mui-footer id="indexPageFooter" v-if="footBarState">
      <mui-footer-item v-for="(item, index) in navBars"
                       :key="index"
                       :label="item.label"
                       :badge="item.badge"
                       active-class="mui-active"
                       :active="currentIndex == index"
                       :icon="item.icon"
                       :index="index"
                       @muiTabClick="muiTabClick(index, item.href)"
      >
      </mui-footer-item>
    </mui-footer>
    <transition name="router-fade" mode="out-in">
			<keep-alive>
			    <router-view></router-view>
			</keep-alive>
    	</transition>
  </div>
</template>
<script>
  require('./public/mui')
  import MuiFooter from './components/common/mui-footer.vue'
  import MuiFooterItem from './components/common/mui-footer-item.vue'
  import MuiHeader from './components/common/mui-header.vue'
  import MuiHeaderBtn from './components/common/mui-header-btn.vue'

  export default {
    components: {
      MuiFooter,
      MuiFooterItem,
      MuiHeader,
      MuiHeaderBtn
    },
    data () {
      return {
        // 底部导航切换切换
        navBars: [
          {label: '首页', icon: 'yk-icon-home', href: '/'},
          {label: '顾客', icon: 'yk-icon-customer', href: '/customer'},
          // {
          //   label: '消息',
          //   icon: 'yk-icon-chatboxes',
          //   href: '/message',
          //   badge: false
          // },
          // {label: '分析', icon: 'yk-icon-chart-pie', href: '/analysis'},
          {label: '我的', icon: 'yk-icon-person', href: '/userinfo'}
        ],
        footerData: {
          index: 0
        },
        test: 1111,
        currentHeader: {
          title: '首页',
          btns: [
            {
              pos: 'left',
              icon: 'mui-icon-left-nav',
              // text: '返回',
              show: false
            }
          ]
        },
      }
    },
    computed: {
      currentIndex () {
        return this.footerData.index
      },
      title () {
        return this.$store.state.title
      },
      footBarState () {
        return this.$store.state.footBarState
      }
    },
    methods: {
      muiTabClick (index, href) {
        this.footerData.index = index
        this.$router.push(href)
      }
    },
    created () {
      let o = {
        'account': 'zxxsjl',
        'password': '123456',
        'remember': false
      }
      this.$store.dispatch('login', o).then(res => {
        console.log(res)
      })
      this.$store.commit('HEADER_TITLE', '我觉得他们很傻逼')
      console.log(this.title)
    },
    watch: {
      '$route' (to, from) {
      }
    }
  }
</script>
