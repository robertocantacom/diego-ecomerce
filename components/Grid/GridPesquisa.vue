<template>
  <div class="">
    <h4>{{ componentTitle }}</h4>
    <div class="btn-novo">
      <button type="button" class="btn btn-primary" @click="novoRegistro()">
        Adicionar Registros
      </button>
    </div>
    <div class="divTable">
      <b-table striped hover responsive :items="dataPesquisa" :fields="fields">
        <template #cell(editar)="row">
          <button
            type="button"
            class="btn btn-secondary"
            @click="editarRegistro(row.item.id)"
          >
            Editar
          </button>
        </template>
      </b-table>
    </div>
    <b-modal ref="meuedit" title="Editar">
      <b-container>
        <CrudFormComponent
          :input-fields="inputFields"
          :get-action="getAction"
          :url="url"
          :registro-id="dataId"
        />
      </b-container>
      <template v-slot:modal-footer="{ hide }">
        <button type="button" class="btn btn-danger" @click="hide()">
          Fechar
        </button>
        <div>
          <button
            type="submit"
            @click="salvarDados(dataId)"
            class="btn btn-success"
          >
            salvar
          </button>
        </div>
      </template>
    </b-modal>
  </div>
</template>

<script>
import { mapState } from 'vuex'
// import barramento from '../barramento'

export default {
  name: 'GridPesquisa',

  props: {
    componentTitle: {
      type: String,
      default: 'Lista',
    },
    label: {
      type: Array,
      default: () => [],
    },
    getAction: {
      type: String,
    },
    fields: {
      type: Array,
      default: () => [],
    },
    inputFields: {
      type: Array,
      default: () => [],
    },
    url: {
      type: String,
    },
  },

  data() {
    return {
      form: {},
      dataPesquisa: [],
      dataId: null,
      clearForm: {},
    }
  },

  computed: {
    ...mapState({
      cli: (state) => state.Cliente.cli,
      cars: (state) => state.Car.cars,
      ord: (state) => state.Ordem.ord,
    }),
  },

  watch: {
    cars(newV, oldV) {
      this.dataPesquisa = newV
    },
    cli(newV, oldV) {
      this.dataPesquisa = newV
    },
    ord(newV, oldV) {
      this.dataPesquisa = newV
    },
  },

  created() {
    this.$root.$on('refreshGrid', (r) => {
      console.log(r)
      this.getData()
    })
  },

  methods: {
    async getData() {
      await this.$store.dispatch(this.getAction)
    },

    editarRegistro(id) {
      this.$refs.meuedit.show()
      this.dataId = id
    },

    novoRegistro() {
      this.$refs.meuedit.show()
      this.dataId = null
    },

    carregamento() {
      this.getData()
    },

    filtermoney(valor) {
      return `R$ ${parseFloat(valor).toFixed(2)}`.replace('.', ',')
    },

    salvarDados(dataId) {
      this.$root.$emit('salvarAlt', dataId)
      this.$refs.meuedit.hide()
    },
  },

  beforeMount() {
    this.carregamento()
  },
}
</script>

<style>
.btn-novo {
  display: flex;
  align-items: right;
  justify-content: right;
  flex-direction: row;
}
</style>
