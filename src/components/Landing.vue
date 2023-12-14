<template>
  <div class="container">
    <div class="Landing">
      <Header/>

      <div class="wrapper">
        <section class="main">
          <h1> Choose, Customize & Publish </h1>
          <p class="grey-color w-75">
            At vero eos et accusamus et iusto odio dignissimos ducimus, qui blanditiis
            praesentium voluptatum deleniti atque corrupti, quos dolores et quas molestias excepturi sint.
          </p>

          <h3 class="mt-2rem">Select Your Plan</h3>
          <div class="plan-select">
            <div class="plan-buttons">
              <button
                @click="setPlanType('Monthly')"
                :class="['plan-btn-default btn-monthly', planType === 'Monthly' && 'plan-btn-active']"
              >
                MONTHLY
              </button>
              <button
                @click="setPlanType('Annual')"
                :class="['plan-btn-default btn-annual', planType === 'Annual' && 'plan-btn-active']"
              >
                ANNUALLY
              </button>
            </div>
          </div>
        </section>

        <aside class="content">
          <PlanView
            :saved-selection="savedSelection"
            :plan-type="planType"
            @openForm="togglePlanForm"
          />
        </aside>
      </div>
    </div>

    <PlanForm
      :plan-type="planType"
      :open-dialog="openDialog"
      @closeForm="togglePlanForm"
      @saveSelection="saveSelection"
    />
  </div>
</template>

<script>
  import Header from './Header.vue';
  import PlanView from './PlanView.vue';
  import PlanForm from './PlanForm.vue';
  
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Landing',
    components: {
      Header, PlanView, PlanForm
    },
    props: {
      msg: String
    },
    data() {
      return {
        planType: 'Monthly',
        openDialog: false,
        savedSelection: false,
      };
    },
    methods: {
      setPlanType(plan) {
        this.planType = plan;
      },
      togglePlanForm() {
        this.openDialog = !this.openDialog;
      },
      saveSelection() {
        this.savedSelection = true;
        this.openDialog = !this.openDialog;
        console.log('Selection Saved!');
      }
    }
  }
</script>

<style>
  h1 {
    font-size: 3em;
  }
  .Landing {
    margin: 0;
    padding: 25px;
  }
  .wrapper {
    display: flex;
    margin-top: 10rem;
  }
  .wrapper section {
    flex: 2;
    padding: 10px 50px;
  }
  .wrapper aside {
    flex: 2;
  }
  .grey-color {
    color: gray;
  }
  .w-75 {
    width: 85%;
  }

  .plan-select {
    display: flex;
    margin-top: -10px;
  }
  button,
  .plan-btn-default {
    border: 1px solid #d8d8d8;
    padding: 15px 25px;
    border-radius: 5px;
    cursor: pointer;
    background: white;
  }
  .plan-btn-active {
    color: white;
    background: #009DFF;
  }
  .btn-monthly {
    border-right: none;
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
  }
  .btn-annual {
    border-left: none;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
  }
  ::-webkit-scrollbar {
    display: none;
  }
</style>
