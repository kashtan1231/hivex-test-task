<template>
  <div class="base-input">
    <input
      class="base-input__field font-weight-400"
      @input="onInput"
      :placeholder="placeholder"
      :type="type"
      :value="value"
    />
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class BaseInput extends Vue {
  @Prop({ default: 'text' }) type!: string
  @Prop({ default: '' }) placeholder!: string
  @Prop({ default: '' }) value!: string
  @Prop({ default: '' }) label!: string
  @Prop({ default: 0 }) maxLength!: number
  @Prop({ default: false }) isNumber!: boolean

  onInput(event: Event): void {
    const target = event.target as HTMLInputElement

    const numberEx = /[^0-9]/g
    if (this.isNumber) {
      target.value = target.value.replace(numberEx, '')
    }

    if (this.maxLength && target.value.length > this.maxLength) {
      target.value = target.value.slice(0, this.maxLength)
    }

    this.$emit('input', target.value)
  }
}
</script>

<style lang="scss" scoped>
.base-input {
  display: flex;
  width: 100%;
  background-color: $blue;
  border-radius: 4px;
  box-shadow: 0px 2px 2px $gray;
  transition-duration: 0.2s;

  &:focus-within,
  &:hover {
    box-shadow: 0px 2px 6px $gray;
  }

  &__field {
    width: 100%;
    padding: 12px 16px;
    outline: none;
    border: none;
    color: $black;
    background: transparent;
    font-size: 16px;
    line-height: 20px;

    &::placeholder {
      font-size: 16px;
      line-height: 20px;
    }
  }
}
</style>
