<script >
export default{
  name: 'App',
  data() {
    return {
      shoppingList: ['Apple', 'Bread', 'Egg']
    };
  }
}
</script>

<template>
  <header>
    <h1><b>Shopping List</b></h1>
  </header>

  <main>
  <div class="row">
    <ul>
      <li v-for="item in shoppingList" :key="index">{{ item }}</li>
    </ul>
  </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
