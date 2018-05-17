<template>
<div>
    <div v-for= "(fighter,index) in myfighters" class="fighter-contain">
        <h1>{{fighter.name}}</h1>
        <img :src= "fighter.image" alt="" class="fighter-img">
        <h2>ATK: {{fighter.attack}}</h2>
        <h2>DEF: {{fighter.defense}}</h2>
        <button @click = "selectFighter(fighter)">Select Fighter</button>

    </div>
</div>
    
</template>

<script>
export default {
name: 'fighters',
    data: function(){
        return {
            name: 'This is a test'
        }
    },

    props: {
        myfighters: Array,
        selectFighter: Function
    }
}
    


</script>

<style>
    .fighter-img {
        max-height: 300px;
    }

    .fighter-contain {
        width: 90%;
        margin: 30px auto;
        border: 2px solid rgba(0, 0, 0 , .6);
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
        text-align: center;
        padding: 20px;
    }
</style>