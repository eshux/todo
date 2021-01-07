<template>
  <div class="todo" :class="checkboxValue && 'done'">
    <input
      :id="id"
      type="checkbox"
      class="checkbox"
      :checked="checkboxValue"
      @change="$emit('onChange')"
    />
    <label :for="id" class="content" :class="checkboxValue && 'done'">{{ todo }}</label>
    <button class="deleteBtn" @click="$emit('onClick')">
      <img class="icon" src="../../assets/x.svg" alt="delete" />
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

const Todo = defineComponent({
  props: {
    checkboxValue: {
      type: Boolean,
      default: false,
    },
    todo: {
      type: String,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
});

export default Todo;
</script>

<style src="./Todo.scss" scoped lang="scss"></style>
