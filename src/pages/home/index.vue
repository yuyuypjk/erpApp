<template>
  <div class="wrapper">
      <div v-if="tabitems[0].visibility">
          <div v-for='menu in menus'>
              <div style="flex-direction: row;">
                  <div v-for='item in menu.data' style="flex:1">
                      <div style="justify-content:center; align-items: center; margin-top: 40px;margin-left: 30px;">
                          <!--<text :style="{fontFamily:'iconfont',color:'white',fontSize:'100px',borderRadius:'25px',backgroundColor:item.bgcolor}" >
                              {{item.icon}}</text>-->
                          <icon
                                 :name="item.icon" :style="[menustyle,{backgroundColor:item.bgcolor}]"></icon>
                          <text style="padding-top: 5px;font-size: 24px;">{{item.name}}</text>
                      </div>

                  </div>
              </div>

          </div>

      </div>

    <div v-if="tabitems[1].visibility">
        <list >
            <cell>
                1
            </cell>
            <cell>
                2
            </cell>
        </list>
    </div>


      <!--<text class="content" v-if="tabitems[0].visibility">TAB 1 的内容111</text>-->

      <!--<text class="content" v-if="tabitems[1].visibility">TAB 2 的内容</text>-->
      <text class="content" v-if="tabitems[2].visibility">TAB 3 的内容</text>

      <tabbar :tabitem = "tabitems" :itemstyle = "itemstyle" @tabItemOnClick="tabItemClick"></tabbar>

  </div>
</template>
<script>
    import icon from '../../components/icon/icon.vue';
   import tabbar from '../../components/tabbar/tabbar.vue';

    import row from '../../components/row/row.vue';
    import CmuiCol from '../../components/col/col.vue';
  import dingtalk from 'weex-dingtalk';
  var modal = weex.requireModule('modal');
  var menuStyle={
      color:'white',
      fontSize:'90px',
      borderRadius:'25px'
  };
    var itemStyle = {
        titleColor: '#000000',
        iconColor:'#666',
        selectedTitleColor: '#ff6a00',
        selectedIconColor: '#ff6a00'
    };
    var menuItems=[
        {data:[{name: '新增采购', icon: 'add-sell', bgcolor: 'green'},{name: '采购订单', icon: 'purchase', bgcolor: '#20A0FF'},{name: '采购入库', icon: 'purchase', bgcolor: '#20A0FF'}]}
       /* {data:[{name: '销售', icon: 'sell',bgcolor: '#13CE66'}]}*/
    ];
    var tabItems =  [{
        title: '首页',
        icon: 'home',
        visibility: true
    },{
        title: '采购',
        icon: 'purchase',
        visibility: false
    },{
        title: '销售',
        icon: 'sell',
        visibility: false
    },{
        title: '码单',
        icon: 'code-order',
        visibility: false
    },{
        title: '库存',
        icon: 'inventory',
        visibility: false
    }];

  export default {
    name: 'home',
      components: {
         icon,
          tabbar,
          row,
          CmuiCol
         // cmuiTabbar: require('gts-weex-components/tabbar')
        //  CmuiIcon: require('gts-weex-components/icon')
          //tabbar:require("weex-tabbar")
         // icon:require('icon')
      },
    data:function(){

         return {
             selectedIndex: 0,
             link: ', author: icepy',
             menus: menuItems,
             menustyle:menuStyle,
             tabitems: tabItems,
             itemstyle: itemStyle

         }
    },
    mounted: function(){
        /*var domModule = weex.requireModule('dom');
        domModule.addRule('fontFace', {
            'fontFamily': "iconfont",
            'src': "url('http://at.alicdn.com/t/font_342201_9ow8z2gk9usg7gb9.ttf')"
        });*/
      dingtalk.ready(function(){
        const dd = dingtalk.apis;
        // 设置导航
        dd.biz.navigation.setTitle({
          title: 'Dingtalk'
        });
      });
    },
      computed: {
              /*getFontName() {
                  return this.decodeIconFont(icons[this.name])
              }*/
          selectIconStyle() {
              let style = {};

              style.color = this.itemstyle.selectedIconColor;

              return style;
          },
          unselectIconStyle() {
              let style = {};

              style.color = this.itemstyle.iconColor;

              return style;
          },
          selectTitleStyle() {
              let style = {};

              style.color = this.itemstyle.selectedTitleColor;

              return style;
          },
          unselectTitleStyle() {
              let style = {};

              style.color = this.itemstyle.titleColor;

              return style;
          }
      },
    methods: {
      getClick: function(){

      },
        tabItemClick: function (e) {
            modal.alert({
                message:'当前tab:' + e,
                okTitle:'ok'
            });
        }
    }
  }
</script>
<style   scoped>
  .wrapper {
    display: flex;
    flex-direction: row;
   /* justify-content: center;*/
    width: 750px;
  }
</style>
