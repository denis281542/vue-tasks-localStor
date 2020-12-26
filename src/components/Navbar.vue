<template>
  <div>
    <nav class="pink darken-1">
      <div class="nav-wrapper">
        <router-link exact to="/" class="brand-logo">Task</router-link>
        <ul id="nav-mobile" class="right hide-on-med-and-down">
          <li>
            <router-link exact to="/create">Create</router-link>
          </li>
          <li>
            <router-link exact tag="a" to="/list">List</router-link>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<style scoped>
  nav {
    padding: 0 5rem;
  }

  a {
    cursor: pointer;
  }

  a.router-link-active {
    background-color: rgba(0,0,0,0.1);
  }

</style>