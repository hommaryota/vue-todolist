<script setup lang="ts">
import { defineProps, toRefs, defineEmits } from 'vue'
const props = defineProps({
  isDisable: { type: Boolean, default: false },
  color: { type: String, required: true },
  cursor: { type: Boolean, required: false }
})
const { isDisable, color } = toRefs(props)
const emit = defineEmits<{
  (e: 'click'): void
}>()
</script>

<template>
  <button
    class="button"
    :style="{ backgroundColor: color, cursor: cursor ? 'pointer' : 'initial' }"
    @click="emit('click')"
    :disabled="isDisable"
  >
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  width: 57px;
  height: 32px;
  background: #c1c1c1;
  border-radius: 4px;
  border: none;
  font: normal normal normal 14px/24px Hiragino Maru Gothic ProN;
  letter-spacing: 0px;
  color: #ffffff;
}
</style>
