<template>
<div class="wayo-lath__content" v-on="$listeners" v-if="show" ref="content">
  <slot>
    <p class="wayo-lath__content-entity" ref="content_entity"
      :class="{'wayo-lath__content_single-line': single_line_content}"
      :style="`${content_oversize?`height:${contentMaxHeight}px;`:''}`"
      @click.stop="ellipsisContent">
      {{content_oversize?content_short:content}}
    </p>
    <p class="wayo-lath__content-hint" v-if='hint'>{{hint}}</p>
    <p class="wayo-lath__content-action" ref="content_action" 
      v-if="showExpandLabel&&content_oversize"
      @click.stop="expandContent">
      {{contentExpandLabel||content_expand_label}}
      <wayo-icon :name="contentExpandIco" v-if="contentExpandIco"/>
    </p>
  </slot>
</div>
</template>

<script>
const CONTENT_FONT_SIZE = 13;
const CONTENT_LINE_HEIGHT = 21;
/**
 * @vue
 */
export default {
  name: `${APPNAME}LathContent`,
  props: {
    /**
     * @prop 内容
     * @type {string}
     * @default ``
     */
    content: {
      type: String,
      default: ''
    },
    /**
     * @prop 内容提示信息
     * @type {string}
     * @default ``
     */
    hint: {
      type: String,
      default: ''
    },
    /**
     * @prop 内容文案的行数限制，超出部分隐藏并显示展开按钮
     * @type {number}
     * @default `3`
     */
    contentLineLimit: {
      type: Number,
      default: 3,
      validator: val => {
        return val>0&&val%1===0;
      }
    },
    /**
     * @prop 内容文案超出行数限制是是够显示展开按钮
     * @type {boolean}
     * @default `false`
     */
    showExpandLabel: {
      type: Boolean,
      default: true
    },
    /**
     * @prop 内容文案超出行数限制是是够显示展开按钮
     * @type {boolean}
     * @default `false`
     */
    hideExpandLabel: {
      type: Boolean,
      default: false
    },
    /**
     * @prop 内容文案展开按钮的文案
     * @type {string}
     * @default `更多`
     */
    contentExpandLabel: {
      type: String,
      default: ''
    },
    /**
     * @prop 内容文案展开按钮的图标
     * @type {string}
     * @default ``
     */
    contentExpandIco: {
      type: String,
      default: ''
    }
  },
  data(){
    return {
      // 是否为单行文案
      single_line_content: false,
      // 超出行数限制时多行文案的缩减版
      content_short: '',
      // 是否超出行数限制
      content_oversize: false,
      // 默认展开文字
      content_expand_label: '',
      // 字体大小
      //font_size: CONTENT_FONT_SIZE,
      // 行高
      //line_height: CONTENT_LINE_HEIGHT
    };
  },
  computed: {
    /**
     * @computed 文案尺寸
     * @type {number}
     */
    contentFontSize(){
      let cont = window.getComputedStyle(this.$refs.content);
      let size = cont&&parseFloat(cont.fontSize);
      return (+size?size:CONTENT_FONT_SIZE);
    },
    /**
     * @computed 多行文案的高度上限
     * @type {number}
     */
    contentMaxHeight(){
      return CONTENT_LINE_HEIGHT*this.contentLineLimit;
    },
    /**
     * @computed 显示状态
     * @type {boolean}
     */
    show(){
      const Result = !!(this.content||(this.$slots.default&&this.$slots.default.length>0));
      return Result;
    }
  },
  watch: {
    content(){
      this.adapteContent();
    },
    show(val){
      this.$parent.hasContent = !!val;
    }
  },
  mounted() {
    //特殊处理
    !this.contentExpandLabel&&!this.contentExpandIco&&(this.content_expand_label='更多');
    //更新宽高
    //window.getComputedStyle(this.$refs.content).fontSize
    //this.font_size = this.$refs.content
    //
    this.adapteContent();
  },
  methods: {
    /**
     * @method adapteContent 适配多行文案
     */
    adapteContent(){
      if(!this.content||!this.$refs.content_entity){
        return;
      }
      this.$nextTick().then(() => {
        const RealHeight = this.$refs.content_entity.offsetHeight;
        // 单行
        if(RealHeight<=CONTENT_LINE_HEIGHT){
          this.single_line_content = true;
          return;
        }
        // 多行
        this.single_line_content = false;
        // 超出行数限制
        //if(RealHeight>this.contentLineLimit*CONTENT_LINE_HEIGHT){
        if(RealHeight>this.contentLineLimit*this.contentFontSize){
          this.content_oversize = true;
          const MaxWidth = Math.floor(this.$refs.content_entity.offsetWidth*this.contentLineLimit);
          if(/[^\x00-\xff]/.test(this.content)){
            let width = 0;
            let index = 0;
            while(width<MaxWidth){
              if(/[^\x00-\xff]/.test(this.content[index])){
                //width+=CONTENT_FONT_SIZE;
                width+=this.contentFontSize;
              }else{
                //width+=CONTENT_FONT_SIZE*0.5;
                width+=this.contentFontSize*0.5;
              }
              index++;
            }
            this.content_short = this.content.substr(0,index-10)+'...';
          }else{
            //this.content_short = this.content.substr(0,Math.floor(MaxWidth/CONTENT_FONT_SIZE-10))+'...';
            this.content_short = this.content.substr(0,Math.floor(MaxWidth/this.contentFontSize-10))+'...';
          }
        }
      });
    },
    /**
     * @method expandContent 展开多行文案
     */
    expandContent(){
      this.content_oversize = false;
    },
    /**
     * @method ellipsisContent 收起多行文案
     */
    ellipsisContent(){
      !this.content_oversize&&this.hideExpandLabel&&(this.content_oversize = true);
    }
  }
};
</script>