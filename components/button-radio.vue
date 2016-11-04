<template>
  <div class="btn-group" data-toggle="buttons">
    <div class="btn"
         :class="[btnVariant, btnSize, item.disabled && 'disabled' || '', value.value == item.value && 'active' || '']"
         @click="changeSelection(item)"
         v-for="item in list">
      {{item.text}}
    </div>
  </div>
</template>

<script>
  export default {
    replace: true,
    computed: {
      btnVariant() {
        return !this.variant || this.variant === `default` ? `btn-secondary` : `btn-${this.variant}`
      },
      btnSize() {
        return !this.size || this.size === `default` ? `` : `btn-${this.size}`
      },
      btnActive() {
        return item.value
      },
    },
    props: {
      value: {
        required: true
      },
      list: {
        type: Array,
        default: [],
        required: true
      },
      size: {
        type: String,
        default: 'md'
      },
      variant: {
        type: String,
        default: 'default'
      },
    },
    methods: {
      changeSelection(item) {
        this.$emit('input', item)
      }
    }
  }
</script>
