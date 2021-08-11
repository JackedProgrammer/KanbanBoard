<template>
    <div class="kanbanContainer">
        <div class="heading">
            <h2 id="title">Kanban Board</h2>
            <add-item-form v-on:reloadList="refreshLists()"></add-item-form>
            
        </div>
        <div class="taskboard">
        <list-view :items="notDoneItems" :headingText="'Tasks'" v-on:reloadList="refreshLists()"/>
        <list-view :items="doneItems" :headingText="'Done'" v-on:reloadList="refreshLists()"/>
        </div>
        
    </div>
</template>

<script>
import addItemForm from './addItemForm.vue';
import listView from './listView.vue';

export default{
    components:{
        addItemForm,
        listView
    },
    data:function(){
        return{
            items:[],
            doneItems:[],
            notDoneItems:[]
        }
    },
    methods:{
        getList(){
            axios.get('/api/items')
            .then(response=>{
                this.items = response.data;
            })
            .catch(err=>{
                console.log(err);
            })
        },
        getNotDoneList(){
            axios.get('/api/items/notdone')
            .then(response=>{
                this.notDoneItems = response.data;
            })
            .catch(err=>{
                console.log(err);
            })
        },
        getDoneList(){
            axios.get('/api/items/done')
            .then(response=>{
                this.doneItems=response.data;
                console.log("loaded items");
            })
            .catch(err=>{
                console.log(err);
            })
        },
        refreshLists(){
            this.getList();
            this.getDoneList();
            this.getNotDoneList();
        }

    },
    created(){
        this.getList();
        this.getDoneList();
        this.getNotDoneList();
    }


}
</script>

<style scoped>
.kanbanContainer{
    margin:auto;
}
.heading{
    background:#e6e6e6;
    padding:1rem;
    width:350px;
    margin:auto
}

.taskboard{
    display: flex;
    flex-direction:row;
    justify-content:space-around
}

#title{
    text-align: center;
}
</style>