<template>
	<div class="row">
    <div class="col s6 offset-s3" v-if="task">
		  <h1>{{task.title}}</h1>

      <form @submit.prevent="editTask">
        <div class="chips" ref="chips"></div>

        <div class="input-field">
          <textarea id="description" v-model="description" class="materialize-textarea"></textarea>
          <label for="description">Description</label>
          <span class="character-counter" style="float: right; font-size: 12px;"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">{{description.length}}/2048</font></font></span>
        </div>

        <input type="text" ref="datepicker">

        <div v-if="task.status !== 'completed'">
          <button class="btn waves-effect waves-light pink darken-1" style="margin-right: 1rem" type="submit">Update task
            <i class="material-icons right">send</i>
          </button>
          <button class="btn waves-effect waves-light blue darken-1" @click="completeTask" type="button">
            Complete task
          </button>
        </div>
      </form>
    </div>
    <p v-else>Task not found</p>
  </div>
</template>

<script>
export default {
  name: 'detail',
  data() {
    return {
      description: '',
      chips: null,
      date: null
    }
  },
  computed: {
    task() {
      return this.$store.getters.taskById(+this.$route.params.id)
    }
  },
  mounted() {
    setTimeout(() => {
      M.updateTextFields()
    }, 0)
    this.chips = M.Chips.init(this.$refs.chips, {
      placeholder: 'Task tags',
      data: this.task.chips
    })
    this.description = this.task.description
    this.date = M.Datepicker.init(this.$refs.datepicker, {
      format: 'dd.mm.yyyy',
      defaultDate: new Date(this.task.date),
      setDefaultDate: true,
      autoClose: true
    });
  },
  methods: {
    editTask() {
      this.$store.dispatch('updateTask', {
        id: this.task.id,
        description: this.description,
        date: this.date.date
      })
      this.$router.push('/list')
    },
    completeTask() {
      this.$store.dispatch('completeTask', this.task.id)
      this.$router.push('/list')      
    }
  },
  destroyed() {
    if(this.chips && this.chips.destroy) {
      this.chips.destroy()
    }
    if(this.date && this.date.destroy) {
      this.date.destroy()
    }
  }
}
</script>