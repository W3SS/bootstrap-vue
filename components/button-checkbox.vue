<template>
  <div class="btn-group" data-toggle="buttons">
    <div class="btn"
         :class="[btnVariant, btnSize, checked(item) > -1 && 'active' || '']"
         v-for="item in list"
         @click="toggleItem(item)"
         :disabled="item.disabled"
    >
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
    },
    props: {
      list: {
        type: Array,
        default: [],
        required: true
      },
      value: {
        type: Array,
        default: [],
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
      toggleItem(item) {
        let v = this.value.slice()
        let index = this.checked(item)
        if (index === -1) {
          v.push(item)
        } else {
          v.splice(index, 1)
        }
        this.$emit('input', v)
      },
      checked(item) {
        if (!this.list) return -1
        return this.value.findIndex(v => v.value === item.value)
      }
    },
  }
</script>
