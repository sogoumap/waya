<template>
<div class="wayo-rate" :style="`font-size:${size}px;`">
  <template v-for="(i,index) in max">
    <div v-if="halfScoreIndex===i" class="wayo-rate__halfbox"
      :key="`halfbox-${index}`"
      :style="`height:${size}px;width:${size}px;line-height:1;font-size:${size}px;`">
      <wayo-icon :name="fillIconName" class="wayo-rate__icon wayo-rate__unchosenColor"  
      :key="`${randomKey}-${i}`"
      :style="`${iconStyle(i)}position:absolute;top:0;left:0;`"/>
      <wayo-icon :name="halfIconName" class="wayo-rate__icon wayo-rate__icon-half wayo-rate__chosenColor" 
        :key="`${randomKey}-${i}-half`"
        :style="`${iconStyle(i)}${chosenColor&&'color:'+chosenColor};`"/>
    </div>
    <wayo-icon :name="fillIconName" :class="['wayo-rate__icon', score>=i?'wayo-rate__chosenColor':'wayo-rate__unchosenColor']" v-else
      :key="`${randomKey}-${i}`"
      :style="iconStyle(i)"/>
  </template>
  <label class="wayo-rate__score" v-if="showScore"
    :style="`font-size:${this.labelSize||this.size}px;`">{{score}}{{scoreLabel}}</label>
</div>
</template>

<script>
import WayoIcon from '@/components/icon';
/**
 * @vue
 */
export default {
  name: `${APPNAME}Rate`,
  props: {
    /**
     * @prop 最大值，即星星个数
     * @type {number}
     * @default `5`
     */
    max: {
      type: Number,
      default: 5
    },
    /**
     * @prop 星星的尺寸
     * @type {number}
     * @default `14`
     */
    size: {
      type: Number,
      default: 14
    },
    /**
     * @prop 初始分值
     * @type {number}
     * @default `0`
     */
    score: {
      type: Number,
      default: 0
    },
    /**
     * @prop 标签文案
     * @type {string}
     * @default `0`
     */
    scoreLabel: {
      type: String,
      default: ''
    },
    /**
     * @prop 标签字体大小
     * @type {number}
     * @default `0`
     */
    labelSize: {
      type: Number,
      default: 0
    },
    /**
     * @prop 显示分值
     * @type {boolean}
     * @default `false`
     */
    showScore: {
      type: Boolean,
      default: false
    },
    /**
     * @prop 选中星星的颜色
     * @type {string}
     * @default `#ed5026`
     */
    chosenColor: {
      type: String,
      default: ''
      //default: '#ed5026'
    },
    /**
     * @prop 未选中星星的颜色
     * @type {string}
     * @default `#d6d6d6`
     */
    unchosenColor: {
      type: String,
      default: ''
      //default: '#d6d6d6'
    },
    /**
     * @prop 完整星星图标
     * @type {string}
     * @default `star-fill`
     */
    fillIconName: {
      type: String,
      default: 'star-fill'
    },
    /**
     * @prop 一半星星图标
     * @type {string}
     * @default `star-half`
     */
    halfIconName: {
      type: String,
      default: 'star-half'
    }
  },
  data(){
    return {
      // 随机key
      randomKey: Math.random().toString(16).split('.')[1]
    };
  },
  computed: {
    /**
     * @computed 不足1分的索引值
     * @type {number}
     */
    halfScoreIndex(){
      if(this.score%1>0){
        return parseInt(this.score)+1;
      }
      return -1;
    }
  },
  methods: {
    /**
     * @method iconStyle 计算icon的样式
     * @param {number} index 索引值
     */
    iconStyle(index){
      var r=[`font-size:${this.size}px;`];
      if(this.score>=index&&this.chosenColor){
        r.push(`color: ${this.chosenColor};`);
      }
      if(this.score<index&&this.unchosenColor){
        r.push(`color: ${this.unchosenColor};`);
      }
      return r.join('');
    }
  },
  components: {
    WayoIcon
  }
};
</script>