<template>
  <div>
    <span class="tooltip-trigger" ref="trigger" @mouseenter="toggle(true)" @mouseleave="toggle(false)"><slot></slot></span>
    <div :class="['tooltip','fade','in',tooltipAlignment]" ref="tooltip">
      <div class="tooltip-inner">
        <div class="tooltip-arrow"></div>
        <div class="tooltip-content">
          <span v-html="text" v-if="text"></span>
          <div class="tooltip-content-wrapper">
            <slot name="content" v-if="!text"></slot>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Tether from 'tether'

export default {
  props: {
    position: {
      type: String,
      default: 'top',
    },
    text: {
      type: String,
      default: '',
    }
  },
  replace: true,
  computed: {
    tooltipAlignment() {
      return !this.position || this.position === `default` ? `tooltip-top` : `tooltip-${this.position}`
    }
  },
  mounted() {
    this._trigger = this.$refs.trigger.children[0]
    this._tooltip = this.$refs.tooltip
    this._tooltip.style.display = 'none'
  },
  methods: {
    toggle(show) {
      if (show) {
        let position = {
          attachment: 'bottom center',
          targetAttachment: 'top center'
        };
        if (this.position === 'bottom') {
          position = {
            attachment: 'top center',
            targetAttachment: 'bottom center'
          }
        }
        if (this.position === 'left') {
          position = {
            attachment: 'middle right',
            targetAttachment: 'middle left'
          }
        }
        if (this.position === 'right') {
          position = {
            attachment: 'middle left',
            targetAttachment: 'middle right'
          }
        }
        this._tooltip.style.display = 'block';
        this._tether = new Tether({
          element: this._tooltip,
          target: this._trigger,
          attachment: position.attachment,
          targetAttachment: position.targetAttachment,
        })
      } else {
        if (this._tether) {
          this._tooltip.style.display = 'none'
          this._tether.destroy()
        }
      }
    },
  },
}
</script>

<style scoped>
.tooltip {
  z-index: 9999;
}
</style>
