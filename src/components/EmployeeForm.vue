<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label>Employee name</label>
            <input
            ref="first" 
            v-model="employee.name" 
            type="text"
            :class="{'has-error': submitting && invalidName}"
            @focus="clearStatus"
            @keypress="clearStatus"
            >
            <label>Employee Email</label>
            <input 
            v-model="employee.email" 
            type="text"
            :class="{'has-error': submitting && invalidEmail}"
            @focus="clearStatus"
            >
            <p v-if="error && submitting" class="error message">
               ❗ Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
              ✅   Employee successfully added
            </p>
            <button class="square-button" id="blue-button">Add Employee</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'employee-form',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            employee: {
                name: '',
                email: '',
            },
        }
    },
    methods: {
        handleSubmit(){
            console.log("testing handlesubmit");
            this.submitting = true;
            this.clearStatus();

            if(this.invalidName || this.invalidEmail){
                this.error = true;
                return;
            }
            this.$emit('add:employee', this.employee);
            this.$refs.first.focus();

            this.employee = {
                name: '',
                email: '',
            }
            this.error = false;
            this.success = true;
            this.submitting = true;
        },
        clearStatus(){
            this.success = false;
            this.error = false;
        }
    },
    computed: {
        invalidName(){
            return this.employee.name === ''
        },
        invalidEmail(){
            return this.employee.email === ''
        },
    }
}
</script>

<style scoped>
form{
    margin-bottom: 2rem;
}

[class*='-message']{
    font-weight: 500;
}

.error-message{
    color: #d33c40;
}

.success-message{
    color: #32a95d;
}
#blue-button{
    background-color: #075f8f;
}
</style>