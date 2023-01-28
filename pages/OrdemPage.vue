<template>
    <div class="row border">
        <div class="col-6 col-md-2"> </div>
        <div class="col-6 col-md-8">
            <br>
            <div class="row">
                <div class="col-6 col-md-12 card">
                    <SearchPesquisaComp :component-title="`Pesquisar Ordem de Venda`" :search-fields="searchFields"
                        get-action="Ordem/getOrd" />
                </div>
            </div>
            <br>
            <div class="row">
                <div class="col-6 col-md-12 card">
                    <GridPesquisa :component-title="`Lista Ordem de Vendas`"
                        get-action="Ordem/getOrd" 
                        :fields="fields"
                        :input-fields="inputFields" :url="url"/>
                </div>
                <PagPagination 
                get-action="Ordem/getOrd" :url="url" :setlist="setlist"/>
            </div>
        </div>
        <div class="col-6 col-md-2 ">
        </div>
    </div>

</template>

<script>

export default {
    components: {
       
    },
    name: 'OrdemPage',

    data() {
        return {
            searchFields: [
                {
                    key: 'nomecli',
                    label: 'Pesquise pelo nome do cliente',
                    required: true,
                    type: 'text',
                },
            ],
            setlist: 'SET_LIST_ORDS',
            url: '/ordemvenda',
            inputFields: [
                {
                    key: 'id',
                    label: 'Id',
                    required: true,
                    type: 'text',
                },
                {
                    key: 'nomecli',
                    label: 'Nome Cliente',
                    required: true,
                    type: 'text',
                },
                {
                    key: 'data',
                    label: 'Data Compra',
                    required: true,
                    type: 'text',
                },
                {
                    key: 'valor',
                    label: 'Valor',
                    required: true,
                    type: 'number',
                },
                {
                    key: 'modelocar',
                    label: 'Modelo Carro',
                    required: true,
                    type: 'text',
                },
            ],

            fields: ['id', 'nomecli', 'data', 'valor', 'modelocar', 'editar']
        }

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