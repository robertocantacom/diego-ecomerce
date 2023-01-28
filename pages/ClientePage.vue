

<template>
    <div class="row border">
        <div class="col-6 col-md-8">
            <br>
            <div class="row">
                <div class="col-6 col-md-12 card">
                    <SearchPesquisaComp :component-title="`Pesquisar Clientes`" :search-fields="searchFields"
                        get-action="Cliente/getClis" />
                </div>
            </div>
            <br>
            <div class="row">
                <div class="col-6 col-md-12 card">
                    <GridPesquisa :component-title="`Lista de Clientes`" get-action="Cliente/getClis"
                        :fields="fields" 
                        :input-fields="inputFields" :url="url"/>
                </div>
            </div>
            <div class="row">
                <PagPagination get-action="Cliente/getClis" :url="url" :setlist="setlist" />
            </div>
        </div>
    </div>
</template>


<script>
import GridPesquisa from '../components/Grid/GridPesquisa.vue';


export default {
    components: {
        GridPesquisa
    },

    name: 'ClientePage',

    data() {
        return {

            setlist: 'SET_LIST_CLIS',
            url: '/clientes',
            inputFields: [
                {
                    key: 'id',
                    label: 'Id',
                    required: true,
                    type: 'text',
                    disabladed: true
                },
                {
                    key: 'nome',
                    label: 'Nome',
                    required: true,
                    type: 'text',
                },
                {
                    key: 'telefone',
                    label: 'Telefone',
                    required: true,
                    type: 'text',
                },
                {
                    key: 'cidade',
                    label: 'Cidade',
                    required: true,
                    type: 'text',
                },
            ],
            searchFields: [
                {
                    key: 'nome',
                    label: 'Pesquise pelo nome do cliente',
                    required: true,
                    type: 'text',
                },
            ],

            fields: ['id', 'nome', 'telefone', 'cidade', 'editar']

        }
    },

    computed: {

    },

    watch: {

    },

    methods: {

    },

    beforeMount() {

    }
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