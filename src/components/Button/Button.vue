<template>
  <button
    class="button"
    :class="{ active: active, fill: type === 'fill' }"
  >
    {{ label }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Button = defineComponent({
  props: {
    label: {
      type: String,
      required: true,
    },
    active: {
      type: Boolean,
      required: false,
    },
    type: {
      type: String,
      required: false,
      validator: (value: string) => value === 'fill',
    },
  },
});

export default Button;
</script>

<style src="./Button.scss" scoped lang="scss"></style>
