<template lang="html">
  <div class="wrap">
    <div class="content content-hasheader content-bottom-tab border-box fullpage">
      <keep-alive>
        <router-view></router-view>
      </keep-alive>
    </div>
    <div class="fixed fixed-bottom nav flex-box">
      <div v-for="(navItem, index) in navItemList" :to="{path: navItem.to}" :key="navItem" class="item text-center nav-item flex-box"  :class="[currentIndex === index ? link_active : link_not_active]" @click="getPosition(navItem,index)">
        <i class="icon iconfont" :class="navItem.icon"></i>
        <a class="title">{{navItem.title}}</a>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
import router from '../../router';
export default {
  data() {
    return {
      navItemList: [
        {
          title: '首页',
          icon: 'icon-home',
          to: 'home'
        },
        {
          title: '会员',
          icon: 'icon-member',
          to: 'member'
        },
        {
          title: '分类',
          icon: 'icon-classify',
          to: 'classify'
        },
        {
          title: '购物车',
          icon: 'icon-shoppingcar',
          to: 'shoppingcar'
        },
        {
          title: '我的',
          icon: 'icon-my',
          to: 'my'
        }
      ],
      currentIndex: 0,
      link_active: 'router-link-active',
      link_not_active: 'no-active',
      indexArr: [
        'home',
        'member',
        'classify',
        'shoppingcar',
        'my'
      ]
    };
  },
  methods: {
    getData() {
      // 获取数据
      // this.$http.get('http://localhost/sportman/activity_home.php')
      //   .then(function (res) {
      //     console.log('res:', res);
      //   }, function (err) {
      //     console.log('err:', err);
      //   });
    },
    getPosition(navItem, index) {
      console.log('index:', index);
      router.push({
        name: navItem.to
      });
      this.storePosition({
        y: document.body.scrollTop || document.documentElement.scrollTop,
        i: this.indexArr[this.currentIndex]
      });
      this.currentIndex = index;
    },
    storePosition(data) {
      window.localStorage.setItem(data.i, JSON.stringify(data));
    }
  },
  created() {
    // 测试获取数据
    // this.getData();
  }
}
</script>

<style type="text/css">
.icon.iconfont {
  font-size: .21rem;
}

.flex-box {
  display: flex;
}

.border-box {
  box-sizing: border-box;
}

.content-bottom-tab {
  padding-bottom: .49rem;
}

.content-hasheader {
  padding-top: .44rem;
}

.fixed {
  position: fixed;
}

.fixed-bottom {
  bottom: 0;
  left: 0;
}

.nav {
  width: 100%;
  background: #FFFFFF;
  flex-wrap: nowrap;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.nav-item {
  width: 100%;
  height: .49rem;
  font-size: .816rem;
  line-height: .49rem;
  color: white;
  flex-direction: column;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
}

.nav-item {
  color: rgba(100, 100, 100, .5);
  font-size: .12rem;
}

.nav-item>.icon.iconfont {
  height: .21rem;
}

.nav-item.router-link-active {
  color: rgba(34, 135, 51, 1);
}

a {
  text-decoration: none;
}

.nav>item {
  flex-grow: 1;
  flex-shrink: 1;
}

.text-center {
  text-align: center;
}
</style>
