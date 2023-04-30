<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <label>Employee name</label>
            <input 
            v-model="employee.name" 
            type="text"
            ref="first"
            :class="{'has-error': submiting && invalidName}"
            @focus="clearStatus"
            @kaypress="clearStatus"
            >
            <br>
            <label for="">Employee email</label>
            <input 
            v-model="employee.email" 
            type="text"
            :class="{'has-error': submiting && invalidEmail}"
            @focus="clearStatus"
            >
            <br>
            <p v-if="error && submiting" class="error-message">
                Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
               Employee Successfuly Added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'employee-form',
    data(){
        return {
            submiting: false,
            error: false,
            success: false,
            employee: {
                name: '',
                email: ''
            }
        }
    },
    methods:{
        handleSubmit(){
            this.submiting = true
            this.clearStatus()
            
            if(this.invalidName || this.invalidEmail){
                this.error = true
                return
            }

            this.$emit('add:employee', this.employee)
            this.$refs.first.focus();

            this.employee = {
                name: '',
                email: ''
            }

            this.error = false
            this.success = true
            this.submiting = false
        },
        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed: {
        invalidName(){
            return this.employee.name === ''
        },
        invalidEmail(){
            return this.employee.email === ''
        }
    }
}
</script>


<style scoped>
form {
    margin-bottom: 2rem;
}

input {
    margin-bottom: 2rem;
}

[class*='-message']{
    font-weight: bold;
}

.error-message{
    color: #d33c40;
}

.success-message{
    color: #32a95d;
}
</style>