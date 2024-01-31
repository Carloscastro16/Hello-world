<script lang="ts" setup>
    import { ref } from 'vue'
    let data: any = ref({
        errors: [],
        values:{
            name: '',
            lastname: '',
            age: 0,
            genderSelect: {
                basicGender: '',
                others: ''
            }
        }
    })
    function checkForm(){
        if(!data.value.values.name){
            data.value.errors.push("Nombre requerido.")
        }else{
            if(data.value.values.name.length > 18){
                data.value.errors.push("Nombre requiere ser menor a 18 caracteres.");
            }
            if(data.value.values.name.length < 5){
                data.value.errors.push("Nombre requiere ser mayor a 5 caracteres.");
            }
        }
        if(!data.value.values.lastname){
            data.value.errors.push("Apellido requerido.")
        }
        if(data.value.values.name == data.value.values.lastname){
            data.value.errors.push("Apellido no puede ser igual al nombre.");
        }
        if(!data.value.values.age){
            data.value.errors.push("Edad requerida.")
        }
        if(!data.value.values.gender){
            data.value.errors.push("Genero requerido.")
        }
        if(data.value.values.age < 0 && data.value.values.age > 60){
            data.value.errors.push("Edades aceptadas solo entre 0 y 60")
        } 
        console.log(data)
    }
    var errorMessages: any = ref({
        name: {
            errors: false,
            message: ''
        },
        lastname: {
            errors: false,
            message: ''
        },
        age: {
            errors: false,
            message: ''
        },
        gender: {
            errors: false,
            message: ''
        }
    })
    
    function nameValidation(name: any){
        console.log(name)
        console.log(name.length)
        if(name.length > 18){
            errorMessages.value.name.errors.value = true
            console.log('Error')
        }
    }
    function lastnameValidation(){
        if(data.value.values.lastname != data.value.values.name){
            errorMessages.value.lastname.errors.value = true
        }
    }
    function ageValidation(age: any){
        console.log(age)
        if(age < 0 || age > 60){
            console.log('Error error')
            return errorMessages.value.age.errors.value = true
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
                <span v-if="errorMessages.name.errors">El nombre debe tener más de 5 caracteres y menos de 18</span>
            </p>
        
            <p class="input-container">
                <label for="age">Apellidos</label>
                <input @input="lastnameValidation()" type="text" name="apellido" id="apellido" v-model="data.values.lastname" min="0">
                <span v-if="errorMessages.lastname.errors">El apellido no puede ser el mismo que el nombre</span>
            </p>
            <p class="input-container">
                <label for="age">Age</label>
                <input @input="ageValidation(data.values.age)" type="number" name="age" id="age" v-model="data.values.age" min="0">
                <span v-if="errorMessages.age.errors">La edad debe estar en el rango entre 0 y 60</span>
            </p>
        
            <p class="input-container">
                <label for="movie">Genero</label>
                <select name="gender" id="gender" v-model="data.values.genderSelect.basicGender">
                <option value="femenino">Femenino</option>
                <option value="masculino">Masculino</option>
                <option value="otro">Otro</option>
                </select>
            </p>
            <input v-if="data.values.genderSelect.basicGender == 'otro'" type="text" v-model="data.values.genderSelect.other">
        
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
    width: 300px;
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
.errors{
    display: flex;
    flex-direction: column;
}
p{
    color: #000;
}
span{
    color: #000;
    opacity: .3;
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
  