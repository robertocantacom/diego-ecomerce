<template>
  <div>
    <div v-if="!loaded">carregando</div>
    <form v-else id="meuform">
      <div
        class="form-group"
        v-for="(field, keyElement) in inputFields"
        :key="keyElement"
      >
        <label>{{ field.label }}</label>
        <input
          class="form-control"
          v-model="form[field.key]"
          :type="field.type"
          :disabled="field.disabladed"
        />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'FormComponent',
  props: {
    inputFields: {
      type: Array,
      default: () => [],
    },
    getAction: {
      type: String,
    },
    url: {
      type: String,
    },
    registroId: {},
  },

  data() {
    return {
      form: {},
      loaded: false,
    }
  },

  created() {
    this.init()
    this.$root.$on('salvarAlt', (e) => {
      console.log('funcionou', e)
      if (e > 0) {
        this.putData()
        console.log('1')
      } else {
        this.postData()
        console.log('0')
      }
    })

    this.$root.$on('clearForm', (clearForm) => {
      console.log(clearForm, 'form clear', this.form)
    })
  },

  methods: {
    async init() {
      if (this.registroId) {
        const data = await this.getData()
        const keys = this.getFields()

        Object.keys(data).forEach((x) => {
          if (keys.includes(x)) {
            this.form[x] = data[x]
            console.log(data[x])
          }
        })
        this.loaded = true
        console.log('dentro do if', this.registroId)
      }
      this.loaded = true
    },

    getData() {
      return this.$axios
        .get(`${this.url}/${this.registroId}`)
        .then((response) => response.data)
    },

    getFields() {
      return this.inputFields.map((x) => x.key)
    },

    async putData() {
      await this.$axios.put(`${this.url}`, this.form)
      this.$root.$emit('refreshGrid', this.form)
    },

    async postData() {
      await this.$axios.post(`${this.url}`, this.form)
      this.$root.$emit('refreshGrid', this.form)
    },
  },
}
</script>

<style></style>
