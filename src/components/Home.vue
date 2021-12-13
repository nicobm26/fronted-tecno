<template>
    <div>holaaa </div>
    <select v-model="tipo"  name="tipo_product">
        <option value="phone13">Phone 13</option>
        <option value="phone12">Phone 12</option>
        <option value="phone11">Phone 11</option>
    </select>
    <input type="text"  v-model="ciudad" placeholder="ciudad">
    <input type="number" v-model="cantidad" placeholder="cantidad">
    <input type="number"  v-model="precio"  placeholder="precio">
    <input type="text"  v-model="celular"  placeholder="celular">
    <input type="text"  v-model="descripcion"  placeholder="descripcion">
    <input type="date"  v-model="fecha"  placeholder="fecha">
    <button v-on:click="crearPedido">Crear pedido </button>
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
            alert(`fecha: ${this.fecha} ${this.username}`);
             this.$apollo.mutate({
                mutation: gql`
                    mutation createOrder($product: OrderInput!){
                        createOrder(product: $product){
                            numeroOrden
                    }
                }`,
                variables: {
                        product: {
                            tipoProducto : this.tipo,
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
                alert('se presento un error   linea 76');
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
.user-info {
    display: grid;
    grid-template-columns: 50% 50%;
    grid-column-gap: 5px;
}

.tabla-transacciones {
    width: 100%;
}
</style>