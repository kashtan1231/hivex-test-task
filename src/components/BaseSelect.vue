<template>
  <div
    class="base-select"
    v-click-outside="closeOptions"
    @click="switchOptions"
  >
    <div class="base-select__wrapper">
      <label class="base-select__wrapper-label">{{ label }}</label>
      <p class="base-select__wrapper-selected-item">
        {{ value || defaultOptionText }}
      </p>
    </div>

    <div class="base-select__arrow"></div>

    <div v-if="isShowOptions" class="options">
      <div
        v-for="item in options"
        class="options__item"
        @click="selectOption(item.name)"
        :key="item.id"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'
import vClickOutside from 'v-click-outside'

@Component
export default class BaseSelect extends Vue {
  @Prop({ default: '' }) value!: string
  @Prop({ default: '' }) label!: string
  @Prop({ default: '' }) defaultOptionText!: string
  @Prop({ default: '' }) options!: Array<unknown>

  isShowOptions = false

  switchOptions(): void {
    this.isShowOptions = !this.isShowOptions
  }
  closeOptions(): void {
    this.isShowOptions = false
  }
  selectOption(name: string): void {
    this.$emit('input', name)
  }

  created(): void {
    Vue.use(vClickOutside)
  }
}
</script>

<style lang="scss" scoped>
.base-select {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 2px 16px 4px;
  background-color: $blue;
  border-radius: 4px;
  box-shadow: 0px 2px 2px $gray;
  transition-duration: 0.2s;
  cursor: pointer;

  &:hover {
    box-shadow: 0px 2px 6px $gray;
  }

  &__wrapper {
    &-label {
      display: block;
      font-size: 12px;
      line-height: 16px;
      color: $gray;
      margin-bottom: 2px;
    }
  }

  &__arrow {
    height: 0;
    margin-left: 8px;
    border-top: 5px solid $black;
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    transition-duration: 0.2s;
  }

  .options {
    position: absolute;
    top: calc(100% + 6px);
    left: 0;
    width: 100%;
    padding: 4px 0;
    background-color: $blue;
    border-radius: 4px;
    box-shadow: 0px 2px 6px $gray;
    max-height: 160px;
    overflow-y: auto;
    z-index: 10;

    &__item {
      padding: 4px 16px;
      transition-duration: 0.2s;
      cursor: pointer;

      &:hover {
        background-color: $gray-blue;
      }
    }
  }
}
</style>
