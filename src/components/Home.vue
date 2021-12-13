<template>
<div class="container"> 
        <h2>Crear pedido</h2>
            <div class="container-input">
        <select v-model="tipoProducto"  name="tipo_product">
            <option value="phone13">Phone 13</option>
            <option value="phone12">Phone 12</option>
            <option value="phone11">Phone 11</option>
        </select>
        <input type="text"  v-model="ciudad" placeholder="ciudad">
        <input type="number" v-model="cantidad" placeholder="cantidad">
        <input type="number"  v-model="precio"  placeholder="precio">
        <input type="text"  v-model="celular"  placeholder="celular">
        <input type="text"  v-model="descripcion"  placeholder="descripcion">
        <!--<input type="date"  v-model="fecha"  placeholder="fecha">-->
        <button class="crear boton" v-on:click="crearPedido">Crear pedido </button>
        <button class="cerrar boton" v-on:click="logOut">Cerrar sesion </button>
        
        </div>
    </div>
</template>
<script>
// import MainLayout from '@/layout/MainLayout.vue'
// import MainLayout from '@/layout/MainLayout.vue'
// import Button from 'primevue/button';
// import InputText from 'primevue/inputtext';
import gql from 'graphql-tag';
export default {
    name: "Home",
    components: {
 
    },
    data: function(){
        // date = new Date().toISOString;
        // console.log(date)
        return {
            tipoProducto : 'phone13',
            ciudad: 'bucaramanga',
            cantidad: '1',
            precio: '1500000',
            celular: '30283212',
            descripcion: 'azul',
            fecha:'2021-11-22T00:49:36.093+00:00',
            username: 'nicol'
        }
    },
    methods: {
        crearPedido: function(){
            alert(`fecha: ${this.fecha} usuario ${this.username}  tipo ${this.tipoProducto}`);
             this.$apollo.mutate({
                mutation: gql`
                    mutation crearPedido($product: OrderInput!){
                        createOrder(product: $product){
                            numeroOrden
                    }
                }`,
                variables: {
                        product: {
                            tipoProducto : this.tipoProducto,
                            ciudad: this.ciudad,
                            cantidad: this.cantidad,
                            precio : this.precio,
                            descripcion : this.descripcion,
                            username : this.username,
                            direccion : this.direccion, 
                            fecha: this.fecha,
                            celular : this.celular
                        }
                }
                }).then((response)=>{
                    alert("felicidades, has realizado tu pedido con exito")
                    console.log(response)
                }).catch((e) => {
                alert('se presento un error   linea 86');
                console.log(e)
                });
        },
        logOut: function() {
            this.$emit('logOut');
        }
    }
}
</script>
<!--
scoped: Van a ser estilos que solamente aplican a este componnete
-->
<style scoped>
body{
    background: rgb(13, 38, 120, 0.2);
}
.container {
    width: 100%;
    height: 80vh;
    position: relative;
    margin: 2em auto;
}
.container h2{
    text-align: center;
    padding: 1em;

}
.container .container-input{
    display: flex;
    flex-direction: column;
    row-gap: 0.5em;
    width: 50%;
    position: relative;
    margin: 1em auto;
    padding: 1em;
    border: 1px solid gray;
}
.container .container-input input{
    height: 3em;
}
.boton{
    display: block;
    height: 40px;
    color:white;
}
.crear{
    background: rgb(13, 38, 120);
}
.cerrar{
    background: rgba(202, 200, 200, 0.979);
    color: black;
}
</style>