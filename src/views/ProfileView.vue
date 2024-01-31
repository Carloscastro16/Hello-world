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
                other: ''
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
        console.log(data.value)
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
        if(name.length > 18 || name.length < 5){
            errorMessages.value.name.errors = true
            console.log('Error')
        }else{
            errorMessages.value.name.errors = false
        }
    }
    function lastnameValidation(){
        if(data.value.values.lastname == data.value.values.name){
            errorMessages.value.lastname.errors = true
        }else{
            errorMessages.value.lastname.errors = false
        }
    }
    function ageValidation(age: any){
        console.log(age)
        if(age < 0 || age > 60){
            console.log('Error error')
            return errorMessages.value.age.errors = true
        }else{
            errorMessages.value.age.errors = false
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
                <span class="input-errors" v-if="errorMessages.name.errors">El nombre debe tener más de 5 caracteres y menos de 18</span>
            </p>
        
            <p class="input-container">
                <label for="age">Apellidos</label>
                <input @input="lastnameValidation()" type="text" name="apellido" id="apellido" v-model="data.values.lastname" min="0">
                <span class="input-errors" v-if="errorMessages.lastname.errors">El apellido no puede ser el mismo que el nombre</span>
            </p>
            <p class="input-container">
                <label for="age">Age</label>
                <input @input="ageValidation(data.values.age)" type="number" name="age" id="age" v-model="data.values.age" min="0">
                <span class="input-errors" v-if="errorMessages.age.errors">La edad debe estar en el rango entre 0 y 60</span>
            </p>
        
            <p class="input-container">
                <label for="movie">Genero</label>
                <select name="gender" id="gender" v-model="data.values.genderSelect.basicGender">
                <option value="femenino">Femenino</option>
                <option value="masculino">Masculino</option>
                <option value="otro">Otro</option>
                </select>
                <input class="gender-input" v-if="data.values.genderSelect.basicGender == 'otro'" type="text" v-model="data.values.genderSelect.other">
            </p>
        
            <p class="submit-container">
                <input @click="checkForm()" type="submit" value="Submit">  
            </p>
            <div v-if="data.errors.length > 0" class="errors">
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
.input-container{
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 100%;
}
.input-container label{
    text-align: left;
    width: 100%;
}
.input-container select{
    width: 100%;
    border-radius: 1rem;
    font-size: .8rem;
    padding: .4rem .5rem;
    border: none;
}
.input-errors{
    color: #fa4545;
    font-size: .7rem;
}
.input-container select:focus-visible{
    outline: none;
    border: none;
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
.submit-container{
    margin-top: 1rem;
}
.submit-container input{
    border-radius: .5rem;
    border: none;
    padding: .4rem 1rem;
}
.input-container input:focus-visible{
    border: none;
    outline: none;
}
.gender-input{
    width: 100%;
    margin-top: 1rem;
}
.errors{
    display: flex;
    flex-direction: column;
}
.errors p{
    color: #000;
}
.errors span{
    color: #fa4545;
    opacity: .6;
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
  