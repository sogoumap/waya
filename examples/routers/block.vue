<template>
<section class="sec fill">
  <p class="title">基本使用</p>
  <wayo-block>
    <wayo-block-content>
      <wayo-block-title>标题</wayo-block-title>
      <p>内容内容内容内容内容内容内容内容内容内容内容</p>
    </wayo-block-content>
  </wayo-block>
  <p class="title">标题栏</p>
  <wayo-block>
    <wayo-block-header>
      标题
    </wayo-block-header>
    <wayo-block-content>
      <wayo-block-title>标题</wayo-block-title>
      <p>内容内容内容内容内容内容内容内容内容内容内容</p>
    </wayo-block-content>
  </wayo-block>
  <p class="title">列表</p>
  <wayo-block>
    <wayo-lath icon="clock" content="内容内容内容内容内容内容内容内容内容内容内容" border-bottom>
      <wayo-lath-content content="内容内容内容内容内容内容内容内容内容内容内容"></wayo-lath-content>
    </wayo-lath>
    <wayo-lath icon="location">
      <wayo-lath-content content="内容内容内容内容内容内容内容内容内容内容内容"></wayo-lath-content>
    </wayo-lath>
  </wayo-block>
  <p class="title">索引</p>
  <wayo-block>
    <wayo-block-content>
      <wayo-block-title>周边找</wayo-block-title>
      <wayo-flex-box justify="space-between">
        <wayo-flex-cell class="search__cell" :span="0">
          美食
        </wayo-flex-cell>
        <wayo-flex-cell class="search__cell" :span="0">
          酒店
        </wayo-flex-cell>
        <wayo-flex-cell class="search__cell" :span="0">
          电影院
        </wayo-flex-cell>
        <wayo-flex-cell class="search__cell" :span="0">
          公交站
        </wayo-flex-cell>
        <wayo-flex-cell class="search__cell" :span="0">
          更多
        </wayo-flex-cell>
      </wayo-flex-box>
    </wayo-block-content>
  </wayo-block>
  <p class="title">自定义内容</p>
  <wayo-block>
    <wayo-lath border-bottom>
      <wayo-lath-header title="评价"></wayo-lath-header>
      <wayo-lath-tail icon="arrow-right" label="1139条"></wayo-lath-tail>
    </wayo-lath>
    <wayo-lath>
      <div class="custom-content">
        <div class="custom-content__header">
          <span class="custom-content__uname">吃货甲</span>
          <div class="custom-content__rate">
            <span class="custom-content__date">4月2号</span>
            <wayo-rate :score="4.5" :size="12"/>
          </div>
        </div>
        <p class="custom-content__content">
          今天邀请石家庄来的宾客，就是工作餐了，现在不能大吃大喝自己请客也不能太破费，不降请客今天邀请石家庄来的宾客，就是工作餐了今天邀请石家庄来...
        </p>
        <wayo-flex-box class="custom-content__gallery">
          <wayo-flex-cell class="custom-content__showcase" :span="3">
            <wayo-image src="http://qcloud.dpfile.com/pc/s-MrVj_kK8JU0i3OfBTLlASXleG8GXUEkZLsklVH3uHtzJ2ui-GuL3NsET4yg0AAGybIjx5eX6WNgCPvcASYAw.jpg" :width="80"/>
          </wayo-flex-cell>
          <wayo-flex-cell class="custom-content__showcase" :span="3">
            <wayo-image src="http://qcloud.dpfile.com/pc/s-MrVj_kK8JU0i3OfBTLlASXleG8GXUEkZLsklVH3uHtzJ2ui-GuL3NsET4yg0AAGybIjx5eX6WNgCPvcASYAw.jpg" :width="80"/>
          </wayo-flex-cell>
          <wayo-flex-cell class="custom-content__showcase" :span="3">
            <wayo-image src="http://qcloud.dpfile.com/pc/s-MrVj_kK8JU0i3OfBTLlASXleG8GXUEkZLsklVH3uHtzJ2ui-GuL3NsET4yg0AAGybIjx5eX6WNgCPvcASYAw.jpg" :width="80"/>
          </wayo-flex-cell>
        </wayo-flex-box>
      </div>
  </wayo-lath>
  </wayo-block>
</section>
</template>
<script>
export default {

};
</script>
<style lang="scss" scoped>
.custom-content__header{
  font-size: 14px;
  line-height: 1;
  margin-bottom: 10px;
}
.custom-content__rate{
  float: right;
}
.custom-content__date{
  display: inline-block;
  vertical-align: middle;
  color: #5f5f5f;
}
.custom-content__content{
  font-size: 13px;
  margin-bottom: 10px;
  line-height: 1.2;
}
.custom-content__showcase{
  font-size: 1px;
  line-height: 1;
}
.search__cell{
  white-space: nowrap;
  background-color: #ed5026;
  height: 60px;
  min-width: 50px;
  text-align: center;
  line-height: 60px;
  border-radius: 4px;
  color: #fff;
}
</style>