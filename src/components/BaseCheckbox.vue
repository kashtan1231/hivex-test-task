<template>
  <div class="base-checkbox" @click="mark">
    <div :class="['base-checkbox__mark', { marked: isMarked }]">✔</div>
    <p :class="['base-checkbox__text', { 'text-marked': isMarked }]">
      {{ text }}
    </p>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class BaseCheckbox extends Vue {
  @Prop({ default: '' }) text!: string
  isMarked = false

  mark(): void {
    this.isMarked = !this.isMarked
    this.$emit('mark', this.isMarked)
  }
}
</script>

<style lang="scss" scoped>
.base-checkbox {
  display: flex;
  cursor: pointer;
  align-items: center;
  width: fit-content;

  &__mark {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 16px;
    height: 16px;
    font-size: 12px;
    color: $white;
    box-shadow: inset 0 0 0 2px $gray;
    border-radius: 2px;
    user-select: none;
    transition-duration: 0.2s;

    &:hover {
      box-shadow: inset 0 0 0 2px $black;
    }
  }

  &__text {
    margin-left: 8px;
    color: $gray;
  }
}

.text-marked {
  color: $black;
}

.marked {
  background-color: $blue-dark;
  box-shadow: inset 0 0 0 2px $black;
}
</style>
