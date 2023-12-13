<template>
  <div class="plan">
    <div class="plan-container">
      <article class="plan-wrapper">
        <p v-if="planType==='M'" class="plan-type">MONTHLY PLAN</p>
        <p v-else class="plan-type">YEARLY PLAN</p>
        <p class="plan-intro">
          Get Started with customizing your plan. You can review edit and pusblish your finished plan with our dedicated controls
        </p>
        <p>Plan Name</p>
        <p>Language</p>
        <p>Quota</p>
        <p>Billing Frequency</p>
        <p>Fare Class</p>
        <p>Price</p>
        <p>Lockin Period</p>

        <button @click="showForm" class="plan-btn-start">GET STARTED</button>
      </article>
    </div>
  </div>
</template>
    
<script>  
 export default {
  name: 'PlanView',
  props: {
    planType: {
      type: String,
      required: true,
    }
  },
  methods: {
    showForm() {
      this.$emit('openForm');
    }
  }
 }
</script>

<style>
  .plan-container {
    display: flex;
    justify-content: center;
    position: relative;
  }
  .plan-wrapper {
    text-align: center;
    padding: 15px 100px;
    width: 400px;
    height: 675px;
    background: white;
    border-radius: 5px;
    border: 1px solid #d8d8d8;
  }
  .plan-type {
    margin-bottom: 2rem;
    color: #009DFF;
    font-size: 1em;
    font-weight: bold;
  }
  .plan-intro {
    margin-bottom: 4rem;
    font-size: 0.9rem;
  }
  .plan-btn-start {
    padding-left: 45px;
    padding-right: 45px;
    background: #009DFF;
    border: none;
    color: white;
    margin-top: 12rem;
  }
  .plan-btn-start:hover {
    background: #0283d3;
    font-weight: bold;
  }
</style>
