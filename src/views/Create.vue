<template>
  <div class="row">
    <div class="col s6 offset-s3">
      <h1>Create task</h1>
    <form @submit.prevent="submit">
      <div class="input-field">
        <input v-model="title" id="title" type="text" class="validate" required>
        <label for="title">Title</label>
        <span class="helper-text" data-error="Title is required"></span>
      </div>

      <div class="chips" ref="chips"></div>

      <div class="input-field">
        <textarea id="description" v-model="description" class="materialize-textarea"></textarea>
        <label for="description">Description</label>
        <span class="character-counter" style="float: right; font-size: 12px;"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">{{description.length}}/2048</font></font></span>
      </div>

       <input type="text" ref="datepicker">

       <button class="btn waves-effect waves-light pink darken-1" type="submit">Create task
        <i class="material-icons right">send</i>
      </button>
    </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'create',
  data() {
    return {
      title: '',
      description: '',
      chips: null,
      date: null
    }
  },
  mounted() {
    M.updateTextFields()
    this.chips = M.Chips.init(this.$refs.chips, {
      placeholder: 'Task tags'
    })
    this.date = M.Datepicker.init(this.$refs.datepicker, {
      format: 'dd.mm.yyyy',
      defaultDate: new Date(),
      setDefaultDate: true,
      autoClose: true
    });
  },
  methods: {
    submit() {
      const task = {
        title: this.title,
        description: this.description,
        id: Date.now(),
        status: 'active',
        chips: this.chips.chipsData,
        date: this.date.date
      }

      this.$store.dispatch('createTask', task)
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