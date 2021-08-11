<template>
    <div class="addItem">
        <div>
            <span>Title: </span>
            <input type="text" v-model="item.title"/>
        </div>
        <span>Description: </span><input type="text" v-model="item.description"/>
        <button 
        :class="[item.title?'active':'inactive','plus']"
        @click="addItem()"
        >+</button>
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            item:{
                title:"",
                description:""
            }
        }
    },
    methods: {
        addItem(){
            if(this.item.title==''){
                return;
            }
            axios.post('api/items/store',{
                item:this.item
            })
            .then(response=>{
                if(response.status==201){
                    this.item.title="";
                    this.item.description="";
                    this.$emit('reloadList');
                }
            })
            .catch(err=>{
                console.log(err);
            })
        }
    }
};
</script>

<style scoped>
.addItem{
    display: flex;
    flex-direction: column;
    margin:auto;
}

input{
    background:#f7f7f7;
    border:0;
    outline:none;
    padding:5px;
    margin-top:5px;
    width:100%;
}

button{
    width:100%;
    padding:5px;
}

.plus{
    font-size:20px;
}

.active{
    color:#00ce25;
}

.inactive{
    color:#999999;
}
</style>