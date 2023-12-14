<template>
  <div class="plan">
    <div class="plan-container">
      <article class="plan-wrapper">
        <div v-if="planType==='Monthly'" class="plan-type">MONTHLY PLAN</div>
        <div v-else class="plan-type">ANNUAL PLAN</div>

        <div v-if="savedSelection">
          <p>Plan Name</p>
          <p>Language</p>
          <p>Quota</p>
          <p>Billing Frequency</p>
          <p>Fare Class</p>
          <p>Price</p>
          <p>Lockin Period</p>

          <button @click="showForm" class="plan-btn-edit">Edit Plan</button>
          &nbsp;&nbsp;&nbsp;&nbsp;
          <button class="plan-btn-publish">Publish Plan</button>
        </div>

        <div v-else>
          <div class="plan-intro">
            Get Started with customizing your plan. You can review, edit and pusblish your selections of personalized information.
          </div>

          <button @click="showForm" class="plan-btn-start">GET STARTED</button>
        </div>
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
    },
    savedSelection: {
      type: Boolean,
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
    padding: 45px 50px;
    width: 375px;
    height: 600px;
    background: white;
    border-radius: 5px;
    border: 1px solid #d8d8d8;
  }
  .plan-type {
    margin-bottom: 0;
    color: #009DFF;
    font-size: 1.5em;
    font-weight: bold;
  }
  .plan-intro {
    font-size: 1.5em;
    margin-bottom: 2rem;
    font-weight: bold;
    margin-top: 12rem;
  }
  .plan-btn-start {
    padding-left: 45px;
    padding-right: 45px;
    background: #009DFF;
    border: none;
    color: white;
    margin-top: 12rem;
  }
  .plan-btn-edit,
  .plan-btn-publish {
    padding-left: 45px;
    padding-right: 45px;
    background: black;
    border: none;
    color: white;
    margin-top: 17rem;
    border: 1px solid black;
  }
  .plan-btn-start:hover,
  .plan-btn-edit:hover,
  .plan-btn-publish:hover {
    background: white;
    font-weight: bold;
    color: black;
  }
</style>
