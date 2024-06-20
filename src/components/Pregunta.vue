<template>
    <img v-if="img" v-bind:src="img" alt="No se puede visualizar la imagen">
    <div class="oscuro">
    </div>
    <div class="pregunta-container">

        <input v-model="pregunta" type="text" placeholder="Hazme una pregunta">
        <p>Recuerda terminar la pregunta con el signo de interrogación (?)</p>

        <div v-show="mensaje" class="respuesta">
            <h2>{{ pregunta }}</h2>
            <h1>{{ respuesta === 'yes'? "SI!":"No!"}}</h1>
        </div>
    </div>
</template>

<script>
export default {

    data() {
        return {
            pregunta: null,
            respuesta: null,
            img: null,
            mensaje:false,
        }
    },
    watch: {
        pregunta(value, oldValue) {
            this.mensaje = false

            console.log({
                value, oldValue
            },);

            if (!value.includes("?")) {
                return;
            }

            this.obtenerRespuesta();
            this.mensaje = true;
        },
    },

    methods: {
        async obtenerRespuesta() {
            this.respuesta = "Pensando....";
            const data = await fetch('https://yesno.wtf/api').then(resp => resp.json());
            console.log(data);
            const { answer, forced, image } = data;
            console.log(answer);
            this.respuesta = answer;
            this.img = image;
            return data;
        }
    },
};
</script>

<style scoped>
img,
.oscuro {
    max-height: 100%;
    height: 100vh;
    max-width: 100%;
    width: 310vh;

    position: fixed;
    top: 0px;
    left: 0px;
}

.oscuro {
    background: rgba(0, 0, 0, 0.25);

    /*0.0 full transparente
    1.0 full opaco */
}

.pregunta-container {
    position: relative;
}

input {
    margin-top: 40px;
    width: 260px;
    padding: 10px 15px;
    border: none;
    border-radius: 15px;
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    z-index: 999;
    /* Asegura que el campo de entrada esté por encima de otros elementos */
}

input:focus {
    outline: none;
}

p,
h1,
h2 {
    color:  #faed27;
}

p {
    font-size: 25px;
    margin-top: 0px;
}

.respuesta {
    margin-top: 120px;
}


</style>