<template>
    <h2>{{presentar}}</h2>
    <p>{{ numero }} <sup>2</sup>={{ calcular }}</p>
    <div>
        <button @click="aumentar">+1</button>
        <button @click="disminuir">-1</button>
    </div>
</template>

<script>
export default {
    props: ["titulo", "num", "contador"],
    data() {
        return {
            numero: 5
        }
    },
    methods: {
        calcularCuadrado() {
            console.log('ingreso al metodo');
            return this.numero * this.numero;
        }
    },
    computed: {
        calcular() {
            console.log('ingreso a la propiedad computada')
            return this.numero * this.numero;

        },
        aumentar() {
            this.numero++;
        },
        disminuir() {
            this.numero--;
        },
        presentar() {
            if (this.titulo !== undefined) {
                return this.titulo
            } else {
                return 'Contador'
            }

        }
    }
}
</script>

<style>
button {
    background: #76c893;
    color: #003049;
    border-radius: 5px;
    border: 2px solid #344e41;
    margin: 5px;
    padding: 5px;
    width: 50px;
    cursor: pointer;
}

button:hover {
    background: #7ae582;
}
</style>