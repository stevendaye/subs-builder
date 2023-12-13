<template>
  <div class="wrapper">
    <footer>
      <ul>
        <li>Companies</li>
        <li>Products</li>
      </ul>
    </footer>
  </div>
</template>
  
<script>  
  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Footer',
  }
</script>
  
<style scoped>
  .wrapper {
    position: absolute;
    bottom: 1rem;
    font-size: 0.8em;
    width: 95%;
  }
  footer{
    display: flex;
    justify-content: center;
    width: 100%;
  }
  ul {
    display: flex;
    margin: 0;
    padding: 0;
  }
  li {
    list-style: none;
    margin-right: 15px;
    cursor: pointer;
  }
</style>
