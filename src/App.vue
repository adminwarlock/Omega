<template>
  <div>
    <v-header v-bind:seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
          <a v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
          <a v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
          <a v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view v-bind:seller="seller" keep-alive></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue';

  const ERR_OK = 0;

  export default {
      data() {
          return {
              seller: {}
          };
      },
      created() {
          this.$http.get('/api/seller').then((response) => {
              response = response.body;
              if (response.errno === ERR_OK) {
                this.seller = response.data;
            };
          });
      },
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .tab
      display:flex
      width:100%
      heigth:40px
      line-height:40px
      border-bottom:1px solid rgba(7,17,27,0.1)
      .tab-item
        flex:1
        text-align:center
        & > a
          display:block
          font-size:14px;
          color:rgb(77,85,93)
          &.active
            color:rgb(240,20,20)

</style>
