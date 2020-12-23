<script>
/**
 * @vue
 */
export default {
  name: `${APPNAME}TabBarLabel`,
  props: {
    /**
     * @prop 尾部图标
     * @type {string}
     * @default ``
     */
    label: {
      type: String,
      default: ''
    },/**
     * @prop 尾部图标颜色
     * @type {string}
     * @default ``
     */
    node: {
      type: Array,
      default: () => []
    },
  },
  render(h){
    return <label class="wayo-tab-bar__label">
      {this.node.length>0&&this.node||this.label}
    </label>;
  }
};
</script>