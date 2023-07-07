<template>
  <div id="app">
    <div class="page">
      <h1 class="page__title">Voice Provisioning</h1>

      <BaseSelect
        v-model="partner"
        label="Select a Partner"
        defaultOptionText="Choose"
        :options="options"
      />

      <BaseInput
        v-model="accountName"
        :isNumber="true"
        placeholder="Account Number"
      />

      <div class="page__grid-auto">
        <BaseInput v-model="firstName" placeholder="First Name" />
        <BaseInput v-model="lastName" placeholder="Last Name" />
      </div>

      <div class="page__grid-auto">
        <BaseInput v-model="address" placeholder="Address" />
        <BaseInput v-model="city" placeholder="City" />
        <BaseInput v-model="state" placeholder="State" />
        <BaseInput v-model="zip" :isNumber="true" placeholder="Zip" />
      </div>

      <div class="page__grid-auto">
        <BaseInput
          v-model="phone"
          :maxLength="11"
          :isNumber="true"
          placeholder="Contact Phone"
        />
        <BaseInput v-model="email" placeholder="Contact Email" />
      </div>

      <div class="page__grid-auto">
        <BaseSelect
          v-model="customerType"
          label="Customer Type"
          defaultOptionText="Choose"
          :options="options"
        />
        <BaseInput
          v-model="provisionNumber"
          :isNumber="true"
          placeholder="Phone Number to Provision"
        />
        <BaseInput
          v-model="password"
          type="password"
          placeholder="Sip Password"
        />
      </div>

      <div class="page__grid-1to2">
        <BaseSelect
          v-model="ported"
          label="Ported"
          defaultOptionText="Choose"
          :options="options"
        />
      </div>

      <div class="page__grid-1to2">
        <BaseCheckbox text="Bypass E911 Adress Automation" @mark="switchMark" />
        <BaseTooltip :text="tooltipText" />
      </div>

      <BaseButton
        class="page__button"
        text="Provision"
        @click.native="provision"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import BaseInput from '@/components/BaseInput.vue'
import BaseSelect from '@/components/BaseSelect.vue'
import BaseCheckbox from '@/components/BaseCheckbox.vue'
import BaseTooltip from '@/components/BaseTooltip.vue'
import BaseButton from '@/components/BaseButton.vue'

@Component({
  components: {
    BaseInput,
    BaseSelect,
    BaseCheckbox,
    BaseTooltip,
    BaseButton
  }
})
export default class App extends Vue {
  partner = ''
  accountName = ''
  firstName = ''
  lastName = ''
  address = ''
  city = ''
  state = ''
  zip = ''
  phone = ''
  email = ''
  customerType = ''
  provisionNumber = ''
  password = ''
  ported = ''
  isMarked = false
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

  get canGoNext(): boolean {
    return Boolean(
      this.partner &&
        this.accountName &&
        this.firstName &&
        this.lastName &&
        this.address &&
        this.city &&
        this.state &&
        this.zip &&
        this.phone &&
        this.email &&
        this.customerType &&
        this.provisionNumber &&
        this.password &&
        this.ported &&
        this.isMarked
    )
  }

  switchMark(emitedMark: boolean): void {
    this.isMarked = emitedMark
  }
  provision(): void {
    if (this.canGoNext) alert('Congrats!')
    else alert('You must fill up form and accept E911')
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

button {
  border: none;
}

#app {
  display: flex;
  align-items: center;
  min-height: 100vh;
  font-family: $font-family-default;
  flex-direction: column;
  width: 100%;
  background-color: $white;
  padding: 20px 40px;
}

.page {
  width: 100%;
  max-width: 1216px;

  > :not(:last-child) {
    margin-bottom: 32px;
  }

  &__title {
    text-align: center;
  }

  &__grid-auto {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    column-gap: 24px;
  }

  &__grid-1to2 {
    display: grid;
    grid-template-columns: calc(33% - 12px) 1fr;
    column-gap: 24px;
  }
}

@media screen and (max-width: 769px) {
  #app {
    padding: 20px 16px;
  }

  .page {
    &__grid-auto,
    &__grid-1to2 {
      display: flex;
      flex-direction: column;

      > :not(:last-child) {
        margin-bottom: 32px;
      }
    }
  }
}
</style>
