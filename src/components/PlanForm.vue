<template>
  <div v-if="openDialog" class="plan-form">
    <div class="plan-form-container">
      <header class="plan-action-btn">
        <button @click="saveForm" class="plan-save-btn">SAVE</button>
        <button @click="closeForm" class="plan-close-btn">X</button>
      </header>
      <form>
        <h2 class="plan-definition-tab">
          Plan Definition
          <span>{{ planType }}</span>
        </h2>
        <div class="columns">
          <div class="column">
            <label
              for="plan-name"
              class="plan-name-label d-block sm-txt mb-10px"
            >
              Plan Name
            </label>
            <input
              type="text"
              id="plan-name"
              class="plan-name-input lx-input mr-5rem"
              v-model="planName"
              placeholder="Name the plan"
              required
            />
            <span v-if="invalidField.planName" class="plan-name-invalidField">
              {{ error.planName }}
            </span>
          </div>

          <div class="column">
            <label
              for="language"
              class="language-label d-block sm-txt mb-10px"
            >
              Language
            </label>
            <select 
              class="language-select lx-input"
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
        <hr/>

        <h2>Billing Definitions</h2>
        <div class="columns">
          <div class="column">
            <label
              for="plan-price"
              class="plan-price-label d-block sm-txt mb-10px"
            >
              Plan Price
            </label>
            <input
              type="text"
              id="plan-price"
              class="plan-price-input lx-input mr-5rem"
              v-model="planPrice"
              placeholder="$999"
              required
            />
            <span v-if="invalidField.planPrice" class="plan-name-invalidField">
              {{ error.planPrice }}
            </span>
          </div>

          <div class="column">
            <label
              for="currency"
              class="currency-label d-block sm-txt mb-10px"
            >
              Currency
            </label>
            <select 
              class="currency-select lx-input"
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
        <hr/>

        <h2>Product Definitions</h2>
        <div class="columns mb-2rem">
          <div class="column mr-7rem">
            <label
              for="trip-type"
              class="trip-type-label d-block sm-txt mb-10px"
            >
              Trip Type
            </label>

            <div class="d-flex">
              <div class="label-input-radio">
                <input
                    type="radio"
                    id="one-way"
                    value="One Way"
                    v-model="pickedTripType"
                />
                <label for="one-way">One Way</label>
              </div>
              &nbsp;&nbsp;&nbsp;&nbsp;

              <div class="label-input-radio">
                <input
                    type="radio"
                    id="roundtrip"
                    value="Roundtrip"
                    v-model="pickedTripType"
                />
                <label for="roundtrip">Roundtrip</label>
              </div>
            </div>
            <span v-if="invalidField.tripType" class="trip-type-invalidField">
              {{ error.tripType }}
            </span>
          </div>

          <div class="column">
            <label
              for="quota-amount"
              class="quota-amount-label d-block sm-txt mb-10px"
            >
              Quota Amount
            </label>
            <input
              type="text"
              id="quota-amount"
              v-model="quotaAmountNumber"
              class="quota-amount-input mr-x5rem sm-input"
              placeholder="1"
            />
            <select
              class="quota-amount-select md-input"
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

        <div class="columns mb-2rem">
          <div class="column mr-2rem">
            <label class="included-routes-label sm-txt">
              Routes included
            </label>

            <div class="plan-routes-btn mt-10px">
              <button
                @click="setRoute('Network')"
                :class="[
                  'plan-btn-network',
                  includedRoute === 'Network' && 'plan-btn-active-route'
                ]"
              >
                All Network
              </button>
              <button
                @click="setRoute('Group')"
                :class="[
                  'plan-btn-group',
                  includedRoute === 'Group' && 'plan-btn-active-route'
                ]"
              >
                A group
              </button>
              <button
                @click="setRoute('Specific')"
                :class="[
                  'plan-btn-specific',
                  includedRoute === 'Specific' && 'plan-btn-active-route'
                ]"
              >
                Specific
              </button>
            </div>
          </div>

          <div class="column">
            <label
              class="lockin-period-label d-block sm-txt mb-10px"
            >
              Lock-in Period
            </label>

            <div class="d-flex mt-15px">
              <div class="label-input-radio">
                <input
                  type="radio"
                  id="six-month"
                  value="6"
                  v-model="pickedLockinPeriod"
                />
                <label id="six-month" for="six-month">
                  6 Months
                </label>
              </div>
              &nbsp;&nbsp;&nbsp;&nbsp;

              <div class="label-input-radio">
                <input
                  type="radio"
                  id="twelve-month"
                  value="12"
                  v-model="pickedLockinPeriod"
                />
                  <label
                    id="twelve-month"
                    for="twelve-month"
                  >
                    12 Months
                </label>
              </div>
            </div>
            <span v-if="invalidField.lockinPeriod" class="lockin-period-invalidField">
              {{ error.lockinPeriod }}
            </span>
          </div>
        </div>

        <div class="columns mb-2rem">
          <div class="column mr-4rem">
            <label class="advance-purchase-label d-block sm-txt mb-10px">
              Advance Purchase (days)
            </label>

            <div class="d-flex items-center">
              <span class="purchase-value">{{ initPurchaseValue }}</span>
              <input v-model="purchaseValue" type="range" min="0" max="30" class="advance-purchase-input" />
              <span class="purchase-value">{{ purchaseValue }}</span>
            </div>
            <span v-if="invalidField.advancePurchase" class="lockin-period-invalidField">
              {{ error.advancePurchase }}
            </span>
          </div>

          <div class="column">
            <label class="booking-window-label d-block sm-txt mb-10px">
              Booking Window (days)
            </label>

            <div class="d-flex items-center">
              <span class="booking-value">{{ initBookingValue }}</span>
              <input v-model="bookingValue" type="range" min="0" max="30" class="booking-window-input" />
              <span class="booking-value">{{ bookingValue }}</span>
            </div>
            <span v-if="invalidField.bookingWindow" class="lockin-period-invalidField">
              {{ error.bookingWindow }}
            </span>
          </div>
        </div>
        
        <div class="columns">
          <div class="column">
            <label
              for="fare-class"
              class="fare-class-label d-block sm-txt mb-10px"
            >
              Fare Class
            </label>
            <input
              type="text"
              id="fare-class"
              v-model="fareClass"
              class="fare-class-input md-input"
              placeholder="$999"
            />
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
    planType: {
      type: String,
      required: true,
    },
    openDialog: {
      type: Boolean,
      required: true,
    }
  },
  data() {
    return {
      planName: '',
      selectedLang: 'Eng',
      planPrice: '',
      selectedCurrency: 'USD',
      pickedTripType: 'One Way',
      quotaAmountNumber: '',
      selectedQuotaAmount: 'per-month',
      includedRoute: 'Network',
      initPurchaseValue: 0,
      initBookingValue: 0,
      pickedLockinPeriod: '6',
      purchaseValue: 10,
      bookingValue: 10,
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
  header.plan-action-btn {
    text-align: right;
  }
  header.plan-action-btn button:first-child {
    color: white;
    background: #009DFF;
    padding-left: 45px;
    padding-right: 45px;
    border-radius: 2px;
    margin-right: 7rem;
  }
  header.plan-action-btn button:last-child {
    position: absolute;
    top: 10px;
    right: 10px;
    color: white;
    border: none;
    border-radius: 100%;
    padding: 5px 8px;
    background: black;
    font-weight: bolder;
  }

  h2 span {
    font-size: 0.5em;
    font-weight: 200;
    color: white;
    padding: 2px 10px;
    border-radius: 25px;
    background: #009DFF;
  }
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
    position: relative;
    background: white;
    color: black;
    z-index: 5;
    opacity: 1;
    max-width: 1200px;
    margin: 0 auto;
    margin-top: 3rem;
    height: 835px;
    border-radius: 4px;
    padding: 50px 50px 0 50px;
  }

  .columns {
    display: flex;
  }
  .d-block {
    display: block;
  }
  .d-flex {
    display: flex;
  }
  hr {
    width: 80%;
    height: 1px;
    border: none;
    background: #d8d8d8;
    margin-top: 1.7rem;
    margin-bottom: 1.5rem;
    margin-left: 0;
  }

  .plan-btn-network,
  .plan-btn-group,
  .plan-btn-specific {
    padding: 10px 20px;
    color: #009DFF;
    border-color: #009DFF;
  }
  .plan-btn-network {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }
  .plan-btn-specific {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
  .plan-btn-group {
    border-left: none;
    border-right: none;
    border-radius: 0;
  }
  .plan-btn-active-route {
    color: white;
    background: #009DFF;
    font-weight: bolder;
  }

  /* Form */
  form {
    width: 750px;
    margin: 0 auto;
    padding-left: 5rem;
  }
  .lx-input {
    width: 225px;
    padding: 8px;
  }
  .md-input {
    width: 100px;
    padding: 8px;
  }
  .sm-input {
    width: 45px;
    padding: 8px;
  }

  /* Text */
  .sm-txt {
    font-size: small;
    font-weight: bolder;
  }

  /* Margins */
  .mb-10px {
    margin-bottom: 10px; 
  }
  .mt-5px {
    margin-top: 5px;
  }
  .mt-10px {
    margin-top: 10px; 
  }
  .mt-15px {
    margin-top: 15px; 
  }
  .mt-2rem {
    margin-top: 2rem; 
  }
  .mb-1rem {
    margin-bottom: 1rem;
  }
  .mb-2rem {
    margin-bottom: 2rem;
  }
  .mr-x5rem {
    margin-right: 0.5rem;
  }
  .mr-2rem {
    margin-right: 2rem;
  }
  .mr-3rem {
    margin-right: 3rem;
  }
  .mr-4rem {
    margin-right: 4rem;
  }
  .mr-5rem {
    margin-right: 5rem;
  }
  .mr-7rem  {
    margin-right: 7rem;
  }
  .mr-9rem  {
    margin-right: 9rem;
  }
  .mr-11rem {
    margin-right: 10rem;
  }

  /* Inputs */
  input[type='radio'] {
    width: 45px;
    height: 22px;
    /* accent-color: #009DFF;*/
  }

  input[type="range"] {
    width: 250px;
    height: 2px;
    background: black;
    appearance: none;
    -webkit-appearance: none;
  }

  .label-input-radio {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .label-input-radio label {
    margin-top: 6px;
    margin-left: -7px;
  }
  .label-input-radio:first-child input,
  .label-input-radio:last-child input {
    margin-left: -12px;
  }
  .items-center {
    align-items: center;
  }
</style>
