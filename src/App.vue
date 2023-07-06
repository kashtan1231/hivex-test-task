<template>
  <div id="app">
    <div class="page">
      <h1 class="page__title">Voice Provisioning</h1>

      <BaseSelect
        label="Select a Partner"
        defaultOptionText="Choose"
        :options="options"
      />

      <BaseInput v-model="accountName" placeholder="Account Number" />

      <div class="page__auto-grid">
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
      </div>

      <div class="page__auto-grid">
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
      </div>

      <div class="page__auto-grid">
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
      </div>

      <div class="page__auto-grid">
        <BaseSelect
          label="Select a Partner"
          defaultOptionText="Choose"
          :options="options"
        />
        <BaseInput v-model="accountName" placeholder="Account Number" />
        <BaseInput v-model="accountName" placeholder="Account Number" />
      </div>

      <div class="page__tooltip">
        <BaseCheckbox text="Bypass E911 Adress Automation" />
        <BaseTooltip :text="tooltipText" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import BaseInput from '@/components/BaseInput.vue'
import BaseSelect from '@/components/BaseSelect.vue'
import BaseCheckbox from '@/components/BaseCheckbox.vue'
import BaseTooltip from '@/components/BaseTooltip.vue'

@Component({
  components: {
    BaseInput,
    BaseSelect,
    BaseCheckbox,
    BaseTooltip
  }
})
export default class App extends Vue {
  accountName = ''
  tooltipText =
    '(By checking "Bypass E911 Address Automation" you agree to manually add this phone number and address to Bandwidth)'
  options = [
    {
      id: 1,
      name: 'one'
    },
    {
      id: 2,
      name: 'two'
    },
    {
      id: 3,
      name: 'three'
    },
    {
      id: 4,
      name: 'four'
    },
    {
      id: 5,
      name: 'five'
    },
    {
      id: 6,
      name: 'six'
    },
    {
      id: 7,
      name: 'seven'
    }
  ]
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  align-items: center;
  height: 100vh;
  font-family: $font-family-default;
  flex-direction: column;
  width: 100%;
  padding: 20px 40px;
}

.page {
  width: 100%;
  max-width: 1216px;

  > :not(:last-child) {
    margin-bottom: 40px;
  }

  &__title {
    text-align: center;
  }

  &__auto-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    column-gap: 24px;
  }

  &__tooltip {
    display: grid;
    grid-template-columns: calc(33% - 12px) 1fr;
    column-gap: 24px;
  }
}
</style>
