<template>
  <div class="Landing">
    <Header/>

    <div class="container">
      <div class="wrapper">
        <section class="main">
          <h1> Choose, Customize & Publish </h1>
          <p class="grey-color w-75">
            At vero eos et accusamus et iusto odio dignissimos ducimus, qui blanditiis
            praesentium voluptatum deleniti atque corrupti, quos dolores et quas molestias excepturi sint.
          </p>
          <div class="plan-select">
            <div class="plan-buttons">
              <button @click="setMonthlyPlan" :class="['plan-default-btn btn-monthly', planType === 'M' && 'plan-active-btn']">MONTHLY</button>
              <button @click="setYearlyPlan" :class="['plan-default-btn btn-yearly', planType === 'Y' && 'plan-active-btn']">ANNUALLY</button>
            </div>
          </div>
        </section>

        <aside class="content">
          <Plans />
        </aside>
      </div>
    </div>

    <Footer/>
  </div>
</template>

<script>
  import Header from './Header.vue';
  import Plans from './Plans.vue';
  import Footer from './Footer.vue';
  
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Landing',
    components: {
      Header, Plans, Footer
    },
    props: {
      msg: String
    },
    data() {
      return {
        planType: 'M'
      };
    },
    methods: {
      setMonthlyPlan() {
        this.planType = 'M'
      },
      setYearlyPlan() {
        this.planType = 'Y'
      }
    }
  }
</script>

<style scoped>
  h1 {
    font-size: 3em;
  }
  .Landing {
    margin: 0;
  }
  .container {
    margin-top: 10rem;
  }
  .wrapper {
    display: flex;
  }
  .wrapper section {
    flex: 2;
    padding: 10px 50px;
  }
  .wrapper aside {
    flex: 2;
    border: 1px solid green;
  }
  .grey-color {
    color: gray;
  }
  .w-75 {
    width: 85%;
  }

  .plan-select {
    display: flex;
    margin-top: 25px;
  }
  .plan-default-btn {
    border: 1px solid grey;
    padding: 15px 25px;
    border-radius: 45px;
    cursor: pointer;
    background: white;
  }
  .plan-active-btn {
    color: white;
    background: rgb(33, 33, 189);
  }
  .btn-monthly {
    border-right: none;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }
  .btn-yearly {
    border-left: none;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
</style>
