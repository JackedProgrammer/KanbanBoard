<template>
    <div class="item">
        <div>
            <input type="checkbox" @change="updateCheck()" v-model="item.completed"/>
            <span>Title : </span><span :class="[item.completed ? 'completed':'','itemText']">{{item.title}}</span>
            <span><button @click="removeItem()" class="trashcan">X</button></span>
        </div>
        <p>Description : {{item.description}}</p>
        <div class="statusbuttons">
            <input type="radio" name='status' value='notStarted'/>
            <span>Not Started</span>
            <input type="radio" name='status' value='inProgress'/>
            <span>In Progress</span>
            <input type="radio" name='status' value='completed'/>
            <span>Completed</span>
        </div>
    </div>
</template>

<script>

export default {
    props: ['item'],
    methods: {
        updateCheck(){
            axios.put('api/items/'+this.item.id,{
                item:this.item
            })
            .then(response=>{
                if(response.status==200){
                    this.$emit('itemchanged');
                }
            })
            .catch(err=>{
                console.log(err);
            })
        },
        removeItem() {
            axios.delete('api/items/'+this.item.id)
            .then(response=>{
                if(response.status==200){
                    this.$emit('itemchanged');
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
.completed {
    text-decoration:line-through;
    color:#999999;
}
.itemText{
    width:100%;
    margin-left:20px;
}
.item{
    display:flex;
    flex-direction:column;
    border:2px solid black;
}
.trashcan{
    background-color:#e6e6e6;
    color:red;
    border:0;
    outline:none;
    cursor: pointer;
}
.statusbuttons{
    display: flex;
    flex-direction:column;
    align-items:center;
}
</style>