<template>
	<div>
		<h1>List </h1>
    <div class="row">
      <div class="input-field col s6">
        <select ref="select" v-model="filter">
          <option value="" disabled selected>Choose your option</option>
          <option value="active">Active</option>
          <option value="outdated">Outdated</option>
          <option value="completed">Completed</option>
        </select>
        <label>Tasks filter</label>
      </div>
    </div>

    <button v-if="filter" class="btn-small red accent-4" @click="filter = null">Clear filter</button>

    <hr>

		<table v-if="tasks.length">
			<thead>
				<th>#</th>
				<th>Title</th>
				<th>Date</th>
				<th>Description</th>
				<th>Status</th>
				<th>Open</th>
			</thead>

      <tbody>
        <tr v-for="(task, idx) in displayTasks" :key="task.id">
          <td>{{idx + 1}}</td>
          <td>{{task.title}}</td>
          <td>{{new Date(task.date).toLocaleDateString()}}</td>
          <td class="width-description">
            <div class="description">{{task.description}}</div>
          </td>
          <td>{{task.status}}</td>
          <td>
            <router-link tag="button" class="btn btn-small red" :to="'/detail/' + task.id" >Open</router-link>
          </td>
        </tr>
      </tbody>
		</table>

		<p v-else>No tasks</p>
	</div>
</template>

<script>

export default {
  data() {
    return {
      filter: null
    }
  },
	computed: {
    tasks() {
      return this.$store.getters.tasks
    },
    displayTasks() {
       return this.tasks.filter(t => {
      	if(!this.filter) {
      		return true
      	}
      	return t.status === this.filter
      })
    }
  },
  mounted() {
    M.FormSelect.init(this.$refs.select);
  }
}
</script>

<style scoped>
  .width-description {
    max-width: 400px;
  }

  .description {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>