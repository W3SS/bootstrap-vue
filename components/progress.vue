<template>
  <progress
    :class="['progress',progressVariant, striped ? 'progress-striped' : '', animated ? 'progres-animated' : '']"
    :value="value"
    :max="max"
    ref="progress">
  </progress>
</template>

<script>
  export default {
    replace: true,
    computed: {
      progressVariant() {
        return !this.variant || this.variant === `default` ? `progress-primary` : `progress-${this.variant}`
      },
    },
    props: {
      animated: {
        type: Boolean,
        default: false,
      },
      max: {
        type: Number,
        default: 100,
      },
      striped: {
        type: Boolean,
        default: false,
      },
      value: {
        type: Number,
        default: 0,
      },
      variant: {
        type: String,
        default: 'default',
      },
    }
  }


</script>
