<template>
    <div class="list">
        <p>{{headingText}}</p>
        <div v-for="(item,index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                v-on:itemchanged="$emit('reloadList')"
            />
        </div>
    </div>
</template>

<script>
import listItem from './listItem.vue';

export default {
    props: ['items','headingText'],
    components: {
        listItem
    }
};
</script>

<style scoped>
.item{
    padding:5px;
    background: #e6e6e6;
    margin:1rem;
}

.list{
    background:lightgray;
    width:20vw;
}

p{
    text-align: center;
}
</style>