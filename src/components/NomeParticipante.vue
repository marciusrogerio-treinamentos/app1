<template>
    <div>
        <div class="row">
            <div class="col-11">
                <div class="input-group mb-3">
                    <span class="input-group-text" id="basic-addon1">{{ indice + 1}}</span>
                    <input type="text" class="form-control" placeholder="informe o nome:" v-model="nome" @blur="updParticipante" >
                </div>       
            </div>    
            <div class="col-1">
                <button type="button" class="btn btn-danger btn-sm circle mb-3" @click="delParticipante">
                    X
                </button>                
            </div>   
        </div>         
    </div>
</template>

<script>
export default {
    props: {
        participante: Object,
        indice: Number
    },
    data() {
        return {
            nome: this.participante.nome,
        }
    },
    methods: {
        delParticipante() {
            this.$emit('delParticipante',this.participante.id)
        },
        updParticipante() {
            this.$emit('updParticipante',this.participante.id, this.nome)
        }
    }

}
</script>