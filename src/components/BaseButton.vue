<template>
  <button class="base-button">
    <p class="base-button__text">{{ text }}</p>
  </button>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class BaseButton extends Vue {
  @Prop({ default: '' }) text!: string
}
</script>

<style lang="scss" scoped>
.base-button {
  padding: 12px 16px;
  width: fit-content;
  background-color: $blue-dark;
  border-radius: 4px;
  transition-duration: 0.2s;
  cursor: pointer;

  &:hover {
    opacity: 0.9;
  }

  &__text {
    color: $white;
    text-transform: uppercase;
  }
}
</style>
