<template>
  <div v-if="openDialog" class="plan-form">
    <div class="plan-form-container">
      <header class="plan-action-btn">
        <button @click="saveForm" class="plan-save-btn">SAVE</button>
        <button @click="closeForm" class="plan-close-btn">X</button>
      </header>
      <form>
        <p class="plan-definition-tab">Plan Definition</p>
        <div class="columns">
          <div class="column">
            <label
              for="plan-name"
              class="plan-name-label"
            >
              Plan Name: {{ planName }}
            </label>
            <input
              type="text"
              id="plan-name"
              class="plan-name-input"
              v-model="planName"
              required
            />
            <span v-if="invalidField.planName" class="plan-name-invalidField">
              {{ error.planName }}
            </span>
          </div>

          <div class="column">
            <label
              for="language"
              class="language-label"
            >
              Language: {{ selectedLang }}
            </label>
            <select 
              class="language-select"
              v-model="selectedLang"
              required
            >
              <option value="Eng">English</option>
              <option value="Fr">French</option>
              <option value="ES">Spanish</option>
              <option value="DE">German</option>
            </select>
            <span v-if="invalidField.language" class="language-invalidField">
              {{ error.language }}
            </span>
          </div>
        </div>

        <p>Billing Definitions</p>
        <div class="columns">
          <div class="column">
            <label
              for="plan-price"
              class="plan-price-label"
            >
              Plan Price:
            </label>
            <input
              type="text"
              id="plan-price"
              class="plan-price-input"
              v-model="planPrice"
              required
            />
            <span v-if="invalidField.planPrice" class="plan-name-invalidField">
              {{ error.planPrice }}
            </span>
          </div>

          <div class="column">
            <label
              for="currency"
              class="currency-label"
            >
              Currency:
            </label>
            <select 
              class="currency-select"
              v-model="selectedCurrency"
              required
            >
              <option value="USD">USD</option>
              <option value="EUR">EUR</option>
            </select>
            <span v-if="invalidField.currency" class="language-invalidField">
              {{ error.currency }}
            </span>
          </div>
        </div>

        <p>Product Definitions</p>
        <div class="columns">
          <div class="column">
            <label
              for="trip-type"
              class="trip-type-label"
            >
              Trip Type: {{ pickedTripType }}
            </label>
            <input
              type="radio"
              id="one-way"
              value="One Way"
              v-model="pickedTripType"
            />
            <label for="one-way">One Way</label>

            <input
              type="radio"
              id="roundtrip"
              value="Roundtrip"
              v-model="pickedTripType"
            />
            <label for="roundtrip">Roundtrip</label>
            <span v-if="invalidField.tripType" class="trip-type-invalidField">
              {{ error.tripType }}
            </span>
          </div>

          <div class="column">
            <label
              for="quota-amount"
              class="quota-amount-label"
            >
              Quota Amount:
            </label>
            <input
              type="text"
              id="quota-amount"
              v-model="quotaAmountNumber"
              class="quota-amount-input"
            />
            <select
              class="quota-amount-select"
              v-model="selectedQuotaAmount"
              required
            >
              <option value="per-month">per month</option>
              <option value="per-year">per year</option>
            </select>
            <span v-if="invalidField.quotaAmount" class="quota-amount-invalidField">
              {{ error.quotaAmount }}
            </span>
          </div>
        </div>

        <div class="columns">
          <div class="column">
            <label class="included-routes-label">Routes included</label>
            <div class="plan-routes-btn">
              <button
                @click="setRoute('Network')"
                :class="['plan-default-btn plan-network-btn', includedRoute === 'Network' && 'plan-active-btn']"
              >
                All Network
              </button>
              <button
                @click="setRoute('Group')"
                :class="['plan-default-btn plan-group-btn', includedRoute === 'Group' && 'plan-ative-btn']"
              >
                A group
              </button>
              <button
                @click="setRoute('Specific')"
                :class="['plan-default-btn plan-specifc-btn', includedRoute === 'Specific' && 'plan-ative-btn']"
              >
                Specific
              </button>
            </div>
          </div>

          <div class="column">
            <label
              class="lockin-period-label"
            >
              Lock-in Period: {{ pickedLockinPeriod }}
            </label>
            <input
              type="radio"
              id="six-month"
              value="6"
              v-model="pickedLockinPeriod"
            />
            <label id="six-month" for="six-month">6 Months</label>

            <input
              type="radio"
              id="twelve-month"
              value="12"
              v-model="pickedLockinPeriod"
            />
            <label id="twelve-month" for="twelve-month">12 Months</label>
            <span v-if="invalidField.lockinPeriod" class="lockin-period-invalidField">
              {{ error.lockinPeriod }}
            </span>
          </div>
        </div>

        <div class="columns">
          <div class="column">
            <label class="advance-purchase-label">Advance Purchase (days)</label>
            <input v-model="purchaseValue" type="range" min="0" max="30" class="advance-purchase-input" />
            <span>{{ purchaseValue }}</span>
            <span v-if="invalidField.advancePurchase" class="lockin-period-invalidField">
              {{ error.advancePurchase }}
            </span>
          </div>
          <div class="column">
            <label class="booking-window-label">Booking Window (days)</label>
            <input v-model="bookingValue" type="range" min="0" max="30" class="booking-window-input" />
            <span>{{ bookingValue }}</span>
            <span v-if="invalidField.bookingWindow" class="lockin-period-invalidField">
              {{ error.bookingWindow }}
            </span>
          </div>
        </div>
        
        <div class="columns">
          <div class="column">
            <label for="fare-class" class="fare-class-label">Fare Class</label>
            <input type="text" id="fare-class" v-model="fareClass" class="fare-class-input"/>
            <span v-if="invalidField.fareClass" class="lockin-period-invalidField">
              {{ error.fareClass }}
            </span>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
    
<script>  
 export default {
  name: 'PlanForm',
  props: {
    openDialog: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      planName: '',
      selectedLang: '',
      planPrice: '',
      currency: '',
      pickedTripType: '',
      quotaAmountNumber: '',
      selectedQuotaAmount: '',
      includedRoute: 'Network',
      pickedLockinPeriod: '',
      purchaseValue: '',
      bookingValue: '',
      fareClass: '',
      invalidField: {
        planName: false,
        language: false,
        planPrice: false,
        currency: false,
        tripType: false,
        quotaAmount: false,
        advancePurchase: false,
        bookingWindow: false,
        fareClass: false
      },
      error: {
        planName: 'The plan name is incorrect',
        language: 'The language field is required',
        planPrice: 'The plan price is incorrect',
        currency: 'The currency field is required',
        tripType: 'The trip type is required',
        quotaAmount: 'The quato amount is incorrect',
        advancePurchase: 'The advance purchase is incorrect',
        bookingWindow: 'The booking window is incorrect',
        fareClass: 'The fare class in incorrect'
      }
    };
  },
  methods: {
    saveForm() {
      console.log('Form Saved!');
    },
    closeForm() {
      this.$emit('closeForm');
      console.log('Form Closed');
    },
    setRoute(route) {
      this.includedRoute = route;
    }
  }
 }
</script>

<style>
  .plan-form {
    position: absolute;
    top: 0;
    left: 0;
    overflow: hidden;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.7);
  }
  .plan-form-container {
    background: white;
    color: black;
    z-index: 5;
    opacity: 1;
    max-width: 1200px;
    margin: 0 auto;
    margin-top: 5rem;
    height: 800px;
    border-radius: 4px;
    padding: 50px 50px 0 50px;
  }
</style>
