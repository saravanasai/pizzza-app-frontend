<script>
export default {
  // Properties returned from data() become reactive state
  // and will be exposed on `this`.
  data() {
    return {
      pizzas: [],
    };
  },

  // Methods are functions that mutate state and trigger updates.
  // They can be bound as event handlers in templates.
  methods: {
    async fetchPizza() {
      let res = await fetch("http://localhost:8000/api/pizzas");
      this.pizzas = await res.json();
    },
  },

  // Lifecycle hooks are called at different stages
  // of a component's lifecycle.
  // This function will be called when the component is mounted.
  mounted() {
    this.fetchPizza();
  },
};
</script>

<template>
  <div>
    <nav class="navbar bg-primary mb-5">
      <div class="container-fluid mx-auto">
        <a class="navbar-brand text-white" href="#">Pizza Shop</a>
      </div>
    </nav>
    <main class="container">
      <div class="row row-cols-3 g-2">
        <div class="col p-2" v-for="pizza in pizzas" :key="pizza.id">
          <div class="card" style="width: 24rem">
            <img
              :src="pizza.image"
              class="card-img-top"
              style="object-fit: none; height: 250px"
              :alt="pizza.name"
            />
            <div class="card-body overflow-y-hidden">
              <h5 class="card-title">{{ pizza.name }}</h5>
              <p class="card-text">
                {{ pizza.description.slice(0, 80) + "..." }}
              </p>
              <a href="#" class="btn btn-primary">Order Now</a>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style></style>
