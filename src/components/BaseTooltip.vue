<template>
  <div class="base-tooltip">
    <div class="base-tooltip__circle">!</div>
    <p class="base-tooltip__text">{{ text }}</p>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class BaseTooltip extends Vue {
  @Prop({ default: '' }) text!: string
}
</script>

<style lang="scss" scoped>
.base-tooltip {
  display: flex;
  cursor: pointer;
  align-items: center;
  width: fit-content;
  padding: 16px 16px 8px;
  box-shadow: inset 0 0 0 1px $orange, inset 0px 8px 0px 0px $orange-light;
  border-radius: 4px;

  &__circle {
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 30px;
    width: 30px;
    height: 30px;
    color: $white;
    font-size: 20px;
    font-weight: 600;
    border-radius: 50%;
    margin-right: 16px;
    background-color: orange;
  }

  &__text {
    color: $orange;
  }
}
</style>
