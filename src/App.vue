<template>
  <div id="app" class="small-container">
    <h1>Local CRUD Using Vue & Primitive UI</h1>
    <employee-form @add:employee="addEmployee"/>
    <employee-table :employees="employees" 
    @delete:employee="deleteEmployee"
    @edit:employee="editEmployee"
    />
    <footer class="text-center">
      <p>© 2020 Made by <a href="yehezkielgunawan123.surge.sh">Yehezkiel Gunawan</a> </p>
      <p>Using resource and knowledge from <a href="https://www.taniarascia.com/getting-started-with-react/">Tania Rascia</a> </p>
    </footer>
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue';
import EmployeeForm from '@/components/EmployeeForm.vue';

export default{
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data(){
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpaper.com'
        },
        {
          id: 2,
          name: 'Ujang',
          email: 'ujang@piedpaper.com'
        },
        {
          id: 3,
          name: 'Ahsanul',
          email: 'anul@piedpaper.com'
        },
      ],
    }  
  },
  methods: {
    addEmployee(employee){
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
      const id = lastId + 1;
      const newEmployee = {...employee, id};

      this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id){
      this.employees = this.employees.filter(
        employee => employee.id !== id
      )
    },
    editEmployee(id, updatedEmployee){
      this.employees = this.employees.map(employee => 
        employee.id === id ? updatedEmployee : employee
      )
    }
  }
}
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;  
}

.small-container{
  max-width: 680px;
}
</style>
