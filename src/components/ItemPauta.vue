<template>
    <div>
        <div class="row" >
            <div class="col-2">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="AC" v-model="localItem.tipo" @blur="updItem">
                </div>  
            </div>
            <div class="col-4">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="Assunto" v-model="localItem.assunto" @blur="updItem">
                </div>  
            </div>            
            <div class="col-1">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="Status" v-model="localItem.status" @blur="updItem">
                </div>  
            </div>   
            <div class="col-2">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="Responsável" v-model="localItem.responsavel" @blur="updItem">
                </div>  
            </div>      
            <div class="col-2">
                <div class="input-group mb-3">
                    <input type="text" class="form-control" placeholder="Prazo" v-model="localItem.prazo" @blur="updItem">
                </div>  
            </div>     
            <div class="col-1">
                <button type="button" class="btn btn-danger btn-sm circle mb-3" @click="delItem">
                    X
                </button>                
            </div>                              
        </div>                    
    </div>
</template>

<script>
export default {
    props: {
        item: Object,
        indice: Number
    },
    data() {
        return {
            localItem: {
                tipo: this.item.tipo,
                assunto: this.item.assunto,
                status: this.item.status,
                responsavel: this.item.responsavel,
                prazo: this.item.prazo
            }
        }
    },
    methods: {
        delItem() {
            this.$emit('delItem',this.item.id)
        },
        updItem() {
            this.$emit('updItem',this.item.id, this.localItem)
        }       
    }   
    
}
</script>