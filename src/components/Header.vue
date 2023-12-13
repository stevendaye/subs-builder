<template>
  <div class="Header">
    <nav>
      <ul class="nav-left">
        <li class="active">Home</li>
        <li>About Us</li>
        <li>Contact Us</li>
      </ul>
      <ul class="nav-right">
        <li class="start">Get Started</li>
        <li class="lang">EN</li>
      </ul>
    </nav>
  </div>
</template>
  
<script>  
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Header',
    props: {
      msg: String
    }
  }
</script>
  
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  nav, ul {
    margin: 0;
    display: flex;
  }
  nav {
    margin: 0;
    padding: 0 50px;
    justify-content: space-between;
  }
 ul {
    margin: 0;
    padding: 0;
  }
  li {
    list-style: none;
    margin-right: 15px;
    cursor: pointer;
  }
  ul li:last-child {
    margin-right: 0;
  }
  .active {
    font-weight: bold;
  }
</style> 