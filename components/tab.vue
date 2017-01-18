<template>
  <div role="tabpanel" class="tab-pane" :class="{active: activeValue, disabled: disabled, fade: fade, in: animate}" v-if="hiddenRender || activeValue">
    <slot></slot>
  </div>
</template>

<script>
export default {
 replace: true,
    data() {
      return {
        fade: this.$parent.fade,
        animate: false,
        activeValue: false,
      }
    },
    props: {
      id: {
        type: String,
        default: ''
      },
      title: {
        type: String,
        default: ''
      },
      active: {
        type: Boolean,
        default: false
      },
      disabled: {
        type: Boolean,
        default: false
      },
      hiddenRender: {
        type: Boolean,
        default: true
      }
    },
    mounted() {
      this.activeValue = this.active;
      const items = this.$parent.items;
      items.push({id: this.id, title: this.title, active: this.activeValue, disabled: this.disabled})
    },
}

</script>
