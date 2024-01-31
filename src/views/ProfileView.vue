<script lang="ts" setup>
    import { ref } from 'vue'
    import type { IFormItems } from '@/interfaces/IFormItems';
    let data: IFormItems = {
        errors: ['Error 1'],
        values:{
            name: '',
            lastname: '',
            age: 0,
            gender: ''
        }
    }
    function checkForm(){
        if(!data.values.name){
            data.errors.push("Nombre requerido.")
        }else{
            if(data.values.name.length > 18){
                data.errors.push("Nombre requiere ser menor a 18 caracteres.");
            }
            if(data.values.name.length < 5){
                data.errors.push("Nombre requiere ser mayor a 5 caracteres.");
            }
        }
        if(!data.values.lastname){
            data.errors.push("Apellido requerido.")
        }
        if(data.values.name == data.values.lastname){
            data.errors.push("Apellido no puede ser igual al nombre.");
        }
        if(!data.values.age){
            data.errors.push("Edad requerida.")
        }
        if(!data.values.gender){
            data.errors.push("Genero requerido.")
        }
        if(data.values.age < 0 && data.values.age > 60){
            data.errors.push("Edades aceptadas solo entre 0 y 60")
        } 
        console.log(data)
    }
    var errorMessages: any = {
        name: {
            errors: ref(false),
            message: ''
        },
        lastname: {
            errors: ref(false),
            message: ''
        },
        age: {
            errors: ref(false),
            message: ''
        },
        gender: {
            errors: ref(false),
            message: ''
        }
    }
    
    function nameValidation(name: any){
        console.log(name)
        console.log(name.length)
        if(name.length > 18){
            errorMessages.name.errors.value = true
        }
    }
    function lastnameValidation(){
        if(data.values.lastname != data.values.name){
            errorMessages.lastname.errors.value = true
        }
    }
    function ageValidation(age: any){
        console.log(age)
        if(age < 0 || age > 60){
            console.log('Error error')
            return errorMessages.age.errors.value = true
        }
    }

</script>

<template>

    <div class="profile">
        <h1>This is an profile page</h1>

        <div class="form">
            
            <p class="input-container">
                <label for="name">Name</label>
                <input @input="nameValidation(data.values.name)" type="text" name="name" id="name" v-model="data.values.name" min="5" max="18">
            </p>
        
            <p class="input-container">
                <label for="age">Apellidos</label>
                <input @input="lastnameValidation()" type="text" name="apellido" id="apellido" v-model="data.values.lastname" min="0">
            </p>
            <p class="input-container">
                <label for="age">Age</label>
                <input @input="ageValidation(data.values.age)" type="number" name="age" id="age" v-model="data.values.age" min="0">
                <span v-if="errorMessages.age.errors">La edad debe estar en el rango entre 0 y 60</span>
            </p>
        
            <p class="input-container">
                <label for="movie">Genero</label>
                <select name="gender" id="gender" v-model="data.values.gender">
                <option value="femenino">Femenino</option>
                <option value="masculino">Masculino</option>
                <option value="otro">Otro</option>
                </select>
            </p>
            <input v-if="data.values.gender == 'otro'" type="text" v-model="data.values.gender">
        
            <p class="submit-container">
                <input @click="checkForm()" type="submit" value="Submit">  
            </p>
            <div class="errors">
                <p>Errores:</p>
                <span v-for="(err, index) in data.errors" :key="index">{{ err }}</span>
            </div>
        </div>
    </div>


</template>
  
<style>
.profile{
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    min-height: 100vh;
}
.form{
    width: fit-content;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: #c4c4c4;
    border-radius: 1rem;
    padding: 1rem;
}
.input-container input{
    font-size: .8rem;
    padding: .4rem .5rem;
    border-radius: 1rem;
    border: none;
    outline: none;
    display: flex;
    flex-direction: column;
}
.input-container label{
    font-size: 1rem;
    color: #000;

}
.input-container input:focus-visible{
    border: none;
    outline: none;
}
@media (min-width: 1024px) {
    .profile {
        display: flex;
        align-items: center;
        width: 100%;
        min-height: 100vh;
    }
}
</style>
  