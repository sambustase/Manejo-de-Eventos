<template>
    <div :class="{container:true}">
        <div :class="{formulario:true}">
            <div :class="{textInput:true}">
                <label v-if="!nombre" class="textRed">Paciente</label>
                <label v-else>Paciente</label>
                <input type="text" v-model="nombre" @input="estadoBoton">
            </div>
            <div :class="{textInput:true}">
                <label v-if="!fecha" class="textRed">Fecha</label>
                <label v-else>Fecha</label>
                <input type="date" v-model="fecha" @input="estadoBoton">
            </div>
            <div :class="{textInput:true}">
                <label v-if="!hora" class="textRed">Hora</label>
                <label v-else>Hora</label>
                <input type="time" v-model="hora" @input="estadoBoton">
            </div>
            <div :class="{textInput:true}">
                <label v-if="!gravedad" class="textRed">Gravedad</label>
                <label v-else>Gravedad</label>
                <select v-model="gravedad" @input="estadoBoton">
                    <option value=""></option>
                    <option value="Baja">Baja</option>
                    <option value="Media">Media</option>
                    <option value="Alta">Alta</option>
                </select>
            </div>
            <div :class="{textInput:true}">
                <label v-if="!motivo" class="textRed">Motivo</label>
                <label v-else>Motivo</label>
                <input type="text" v-model="motivo" @input="estadoBoton">
            </div>
        </div>
        <div>
            <button :disabled="botonDesabilitado" @click="agregarCita">Agregar</button>
        </div>
        <div v-if="citas.length !== 0">
            <div v-for="(cita, index) in citas" :key="index" >
                <div :class="['cita-card', cita.gravedad.toLowerCase()]">
                    <h3>Paciente: {{ cita.nombre }}</h3>
                    <p>Fecha: {{ cita.fecha }}</p>
                    <p>Hora: {{ cita.hora }}</p>
                    <p>Gravedad: {{ cita.gravedad }}</p>
                    <p>Motivo: {{ cita.motivo }}</p>
                    <button @click="eliminarCita(index)">Eliminar</button>
                </div>
            </div>
        </div>
        
    </div>        
</template>

<script>
export default {
    name:"Registro",
    data(){
        return{
            nombre:"",
            fecha:"",
            hora:"",
            gravedad:"",
            motivo:"",
            botonDesabilitado:true,
            citas: [],
        }
    },
    methods:{
        estadoBoton(){
            this.botonDesabilitado = !(this.nombre.trim() && this.fecha && this.hora && this.gravedad && this.motivo.trim()); 

        },
        agregarCita() {
            const nuevaCita = {
                nombre: this.nombre,
                fecha: this.fecha,
                hora: this.hora,
                gravedad: this.gravedad,
                motivo: this.motivo
            };
            this.citas.push(nuevaCita); 
            this.limpiarFormulario(); 
        },
        limpiarFormulario() {
            this.nombre = "";
            this.fecha = "";
            this.hora = "";
            this.gravedad = "";
            this.motivo = "";
            this.botonDesabilitado = true;
        },
        eliminarCita(index) {
            this.citas.splice(index, 1);
        }
    }
    
        
}
</script>

<style scope>
.container {
    border: solid;
    padding: 20px;
    border-radius: 10px;
}
.formulario {
    display: flex;
    margin-bottom: 20px;  
}
.textInput {
    display: flex;
    flex-direction: column;
    margin-right: 20px;
}
.textRed {
    color: red;
}
.boxCita{
    display:flex;
}
.cita-card {
    border: solid;
    border-radius: 5px;
    padding: 10px;
    margin: 10px 0;
    width: 200px;
    height: 300px;
}
.cita-card.baja {
    background-color: green;
    color: white;
}
.cita-card.media {
    background-color: yellow;
}
.cita-card.alta {
    background-color: red;
    color: white;
}
</style>