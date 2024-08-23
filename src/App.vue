<template>
  <div class="bg">
    <the-header />
    <main class="grid-container">
      <section class="grid-container__sidebar">
        <sidebar />
      </section>
      <section class="grid-container__table">
        <clients-block />
      </section>
    </main>
    <sidebar class="mobile-footer" />
  </div>
</template>


<script>
import TheHeader from './components/TheHeader.vue';
import Sidebar from './components/Sidebar.vue';
import ClientsBlock from './components/ClientsBlock.vue';

  export default {
    components: {
      TheHeader,
      Sidebar,
      ClientsBlock
    }
    
  }
</script>


<style lang="scss" scoped>
@import '@/assets/scss/mixins';
@import '@/assets/scss/variables';

.bg {
  min-width: 1240px;
  background-color: $neutral-200;
  padding: 0 30px;
}

.grid-container {
  display: flex;
  margin-top: 30px;
  box-sizing: border-box;

  &__sidebar {
    margin-right: 30px;
  }

  &__table {
    width: 100%;
  }
}

.mobile-footer {
  display: none;
}

@media (max-width: 1240px) {
  .bg { 
    min-width: 100%;
  }
    
}

@media(max-width: 780px) {
  .grid-container {
     &__sidebar { 
      margin: 0;
    }
  }
}

@media(max-width: 500px) {
  .bg {
    padding: 0%;
  }

  .grid-container {  
    padding: 0 15px;
    &__sidebar {
      display: none
    }
  }

  .mobile-footer {
    position: fixed; 
    bottom: 0; 
    left: 0;
    display: flex;
    width: 100%;
    padding: 15px;
  }
}
</style>