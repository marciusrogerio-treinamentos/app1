<template>
    <div class="container">
        <div class="row mb-3" >
            <div class="col-12 header">
                <div class="">ATA DE REUNIÃO</div>
            </div>
        </div>
        <!-- Objetivo -->
        <DadosAta/>

        <!-- Participantes -->
        <div class="row mb-3 sub-header" >
            <div class="col-2 pt-2 pb-2">
                <button type="button" class="btn btn-primary btn-sm" @click="addParticipante">
                    Adicionar participante
                </button>
            </div>            
            <div class="col-10 ">
                <div class="">PARTICIPANTES</div>
            </div>
        </div>    
        <NomeParticipante
            v-for="(participante, index) in participantes"
            :key="participante.id"
            :participante="participante"    
            :indice="index"    
            @delParticipante="delParticipante"
            @updParticipante="updParticipante"
        />


        <!-- Pauta    -->
        <div class="row mb-3 mt-2 sub-header" >
            <div class="col-2 pt-2 pb-2">
                <button type="button" class="btn btn-primary btn-sm" @click="addItem">
                    Adicionar Assunto
                </button>
            </div>
            <div class="col-10">
                <div class="">PAUTA</div>
            </div>
        </div>      
    
        <!-- <div class="row">
            <div class="col-2"><strong>Tipo</strong></div>
            <div class="col-4"><strong>Assunto</strong></div>
            <div class="col-1"><strong>Status</strong></div>
            <div class="col-2"><strong>Responsável</strong></div>
            <div class="col-2"><strong>Prazo</strong></div>
            <div class="col-1"><strong></strong></div>            
        </div> -->

        <ItemPauta
            v-for="(item,index) in itens"
            :key="item.id"
            :item="item"
            :indice="index"
            @delItem="delItem"
            @updItem="updItem"
        />

    </div>
</template>

<script>
import NomeParticipante from '@/components/NomeParticipante.vue'
import ItemPauta from '@/components/ItemPauta.vue'
import DadosAta from '@/components/DadosAta.vue'
export default {
    // *** COMPONENTES IMPORTADOS
    components: {
        DadosAta,
        NomeParticipante,
        ItemPauta
    },
    // *** DADOS LOCAIS
    data() {
        return {
            participantes: [],
            itens: []
        }
    },
    //WATCHS
    watch: {

    },
    // HOOKS
    created() {
        // Adiciona o campo para informar o 1o participante
        // this.participantes.push({
        //     id: 1,
        //     nome: ""
        // })

        // Adiciona o campo para informar o 1o assunto
        // this.itens.push({
        //     id: 1,
        //     tipo: "",
        //     assunto: "",
        //     status:"",
        //     responsavel: "",
        //     prazo: ""
        // })
    },
    // *** METODOS
    methods: {
        // ### PARTICIPANTES ### ------------------------------------------------------------------------------------
        // Adiciona participante no array
        addParticipante() {
            const newParticipante = {
                id: this.participantes.length + 1,
                nome: ''
            }

            // Verifica o último índice
            const ultimoIndice = this.participantes.length - 1

            // Se já tiver dados no array de partcipantes
            if(ultimoIndice > - 1) {
                // Se o campo nome do último item da lista estiver preenchido
                if(this.participantes[ultimoIndice].nome != "") {         
                    // Adiciona campo para preencher o participante      
                    this.participantes.push(newParticipante)
                }
            } else {
                // Se não tiver nenhum dado no array de participantes adiciona campo para ser preenchido
                this.participantes.push(newParticipante)
            }

        },
        // Remove participante do array
        delParticipante(id) {
            const indice = this.participantes.findIndex(item => {   
                return item.id === id
            })

            this.participantes.splice(indice,1)

        },
        // Atualiza o nome do participante no array
        updParticipante(id,nome) {
            const indice = this.participantes.findIndex(item => {
                return item.id === id
            })

            this.participantes[indice].nome = nome
        },
        // ### ASSUNTOS ### --------------------------------------------------------------------------------
        // Adiciona assunto no array
        addItem() {
            const newItem = {
                id:  this.itens.length + 1,
                tipo: "",
                assunto: "",
                status:"",
                responsavel: "",
                prazo: ""
            }                    

            this.itens.push(newItem)

            //console.log(this.itens)
        },
        // Remove item do array
        delItem(id) {
            const indice = this.itens.findIndex(item => {   
                return item.id === id
            })

            this.itens.splice(indice,1)
        },
        // Atualiza os dados do Item no array
        updItem(id,dados) {
            const indice = this.itens.findIndex(item => {   
                return item.id === id
            }) 
            
            this.itens[indice] = dados

        }
    },

}
</script>

<style scoped>
.header {
    background-color: black;
    color: white;
    padding: 7px;
    font-weight: bolder;
    margin-bottom: 3px;
}
.sub-header {
    background-color:black;
    color: white;
    padding: 1px;
    font-weight: bolder;
    margin-bottom: 3px;
    display: flex;
    align-items: center;
}

.xxx {
    display: flex;
    align-items: center;    
    justify-content: center;
}
</style>