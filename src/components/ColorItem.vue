<template>
    <div class="panel__item"
    :class="clase" :id="color" @click="classreturn()">
    </div>
</template>
<script>
export default{
    name:'ColorItem',
    props:{color: String},
    data(){
        return{clase:''}
    },
    methods:{
        classreturn(){
            this.$emit('choose',this.color);
            this.clase = 'animate__bounceIn';
            setTimeout( () => this.clase = '',500);
        }
    }
}
</script>
<style >


.panel__item{ 
        width: 200px;
        height: 200px;
    }
    
</style>