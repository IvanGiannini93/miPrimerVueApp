<script setup>
    import { ref } from 'vue';
    import { computed } from 'vue';

    const name = 'Vue dinamico';
    const styleColor = "color: blue";
    const arrayCoilores = ["blue", "red", "green", "orange"];
    const activo = true;
    const frutas = [
        {
            name: "Manzana",
            price: "$1.5",
            description: "Una fruta deliciosa y nutritiva, perfecta para ensaladas o como snack.",
            stock : 0,
        },
        {
            name: "Plátano",
            price: "$0.75",
            description: "Una fruta dulce y energética, ideal para batidos o como postre.",
            stock : 10,
        },
        {
            name: "Naranja",
            price: "$1.0",
            description: "Una fruta cítrica rica en vitamina C, excelente para jugos o simplemente para comer.",
            stock : 20,
        },
        ];
    const frutaObj = {
        name: "Naranja",
        price: "$1.0",
        description:"una fruta",
        id : 1,
    };
    const arrayNros = ref([]);
    let contador = ref(0);


    /*############## METODOS ############*/
    const handleClick = (mensaje) => {
        console.log(mensaje);
    };

    const increment = () => {
        contador.value++;
    };
    const decrease = () => {
        contador.value--;
    };
    const reset = () => {
        contador.value = 0;
    };
    const addNro = () => {
        arrayNros.value.push(contador.value);
    }


    /*############# COMPUTED ################*/
    const pintarCont = computed( () => {
        if(contador.value > 0){
            return "positive";
        } 
        else if(contador.value < 0){
            return "negative";
        }
        else{
            return "zero";
        }
    });

    const existsInArray = computed( () => {
        return arrayNros.value.includes(contador.value);
    });

</script>

<template>
    <div class="container text-center mt-3">
        <h1>Hola {{ name.toUpperCase() }}</h1>
      <!--  <h2>{{ arrayCoilores }}</h2>
        <h2 v-bind:style="`color: ${arrayCoilores[2]}`">Soy azul</h2>
         <h2 :style="styleColor">Soy azul</h2> v-bind: se puede abreviar con : 
        <h2>{{ activo ? 'estoy activo' : 'estoy inactivo' }}</h2>
        <p v-if = "activo === true">Estoy activo</p>
        <p v-else-if = "activo === false">Estoy inactivo</p>
        <p v-else>Estoy indeciso</p>
    
        <h2 v-show="activo">Estoy activo v-show</h2> 
    
        <ul>
            <li v-for="(color, index) in arrayCoilores" :key="index">
                {{index}} - {{ color }}
            </li>
        </ul>
    
        <ul>
            <li v-for="fruta in frutas" :key="fruta.name">
                {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
            </li>
        </ul> 
        <ul>
            <li v-for="(value, propiedad, index) in frutaObj" :key="value">
                {{ index }} - {{ propiedad }} : {{ value }}
            </li>
        </ul> 
    
        <ul>
            <template v-for="item in frutas" :key="item.name">
                <li v-if="item.stock > 0">
                    {{ item.name }} : {{ item.price }}
                </li>
            </template>
        </ul>
    
        <button v-on:click="handleClick('boton izquierdo')">Activame 1</button>
        <button @click.middle="handleClick('boton del medio')">Activame 2</button>
        <button @click.right.prevent="handleClick('boton derecho')"> activame 3</button> -->
    
        <h2 :class="pintarCont">Contador: {{ contador }}</h2>
        <div class="btn-group">
            <button @click="increment()" class="btn btn-success">Incrementar</button>
            <button @click="decrease()" class="btn btn-danger">Decrementar</button>
            <button @click="reset()" class="btn btn-secondary">Resetear</button>
            <button :disabled="existsInArray" @click="addNro()" class="btn btn-primary">Agregar</button>
        </div>
    
        <div>
            <h2>Lista de favoritos!</h2>
            <ul class="list-group mt-4">
            <li class="list-group-item" v-for="nro in arrayNros">
                {{ nro }}
            </li>
        </ul>
        </div>
    </div>
    
</template>

<style>
    h1{
        color: rgb(15, 0, 185);
    }
    .positive{
        color: green;
    }
    .negative{
        color: red;
    }
    .zero{
        color: black;
    }
</style>