<template>
  <div class="about">
    <div class="d-flex justify-content-between">
      <div>
        <h1>{{ user.name }}</h1>
        <h6>{{ user.email }}</h6>
      </div>
      <div>
        <router-link :to="{ name: 'home' }">
          Voltar
        </router-link>
      </div>
    </div>

    <div
      v-for="todo in user.todos"
      :key="todo.id"
      class="card mb-3"
    >
      <div class="card=body">
        <div class="d-flex justify-content-between">
          <div>
            <h6 class="mb-0">{{ todo.title }}</h6>
            <small class="text=muted">{{ todo.description }}</small>
          </div>
          <div class="ml-auto">
            <i 
              v-if="todo.is_done == true"
              class="fa fa-square"></i>
            <i
              v-else
              class="fa fa-check-square"></i>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        user: {},
      };
    },

    mounted() {
      const userId = this.$route.params.id
      fetch(`http://localhost:8000/api/users/${userId}`)
      .then(response => response.json())
      .then(res => this.user = res.data);
    }
  }

</script>
