<template>
  <div class="plan">
    <div class="plan-container">
      <article class="plan-wrapper">
        <p>Plan Name</p>
        <p>Language</p>
        <p>Quota</p>
        <p>Billing Frequency</p>
        <p>Fare Class</p>
        <p>Price</p>
        <p>Lockin Period</p>
      </article>
    </div>
  </div>
</template>
    
<script>  
 export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Plans',
  props: {
    msg: String
  },
 }
</script>

<style>
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }

  .plan-container {
    display: flex;
    justify-content: center;
  }
  .plan-wrapper {
    width: 625px;
    height: 675px;
    background: white;
    border-radius: 5px;
  }
</style>
