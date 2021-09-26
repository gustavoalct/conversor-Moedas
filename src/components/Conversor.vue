<template lang="">
    <div class="conversor">
        <!-- COMPONENTE--> 
        <h2>{{moedaA}} para {{moedaB}}</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder = "moedaA">
        <input type="button" value="Converter" v-on:click="converter"> 
        <h2>{{moedaB_value}} </h2> 
        <br> <br> 


    </div>
</template>

<script>

export default {
    name: "conversor",
    props:["moedaA","moedaB"],

    // criando uma funcao 
    data(){
        return{
            moedaA_value : "", // liga no input text  
            moedaB_value : 0
        };
    },

    methods:{
        // funcao converter o valor
            converter(){
                // api para converter
                let de_para = this.moedaA + "_" + this.moedaB;
               
                let url = "https://free.currconv.com/api/v7/convert?q=" + de_para + "&compact=ultra&apiKey=82f7e51f93c134546a6a";

                //console.log(de_para),
               
                // fecth requisicao
                fetch(url)
                    .then(res => { return res.json();}).then(json => {let cotacao = json[de_para];
                    this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
                    console.log(cotacao)
                });     
                     
            }    
     }
};

</script>



<style scoped>
    
</style>