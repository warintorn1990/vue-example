<template>
  <div id="app" class="small-container">
   <h1>Employees</h1>
   <employee-form @add:employee="addEmployee" />
   <employee-table v-bind:employees="employees" 
   @delete:employee="deleteEmployee" 
   @edit:employee="editEmployee"
   />
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable'
import EmployeeForm from '@/components/EmployeeForm'
export default {
  name: 'App',
  components: { EmployeeTable, EmployeeForm },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Warintorn Wiboonsin',
          email: 'warin@gmail.comn'
        },
        {
          id: 2,
          name: 'Boonyarit Wongsombat',
          email: 'jj@gmail.comn'
        },
        {
          id: 3,
          name: 'Thodsaporn Thongrat',
          email: 'tod@gmail.comn'
        },
      ]
    }
  },
  methods: {
    addEmployee(employee){
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id: 0;
      const id = lastId +1;
      const newEmployee = { ...employee, id };
      this.employees= [...this.employees, newEmployee]
      console.log(employees)
    },
    deleteEmployee(id){
     this.employees = this.employees.filter(employee => employee.id !== id)
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map(employee => employee.id === id ? updatedEmployee: employee)
    }
  }
}
</script>

<style>

button{
  background: #009435;
  border: 1px solid  #009435;
  padding: .5em;
  color: #fff;
}

button:hover,
button:active,
button:focus{
  background: #009435;
  border: 1px solid  #009435;
}
.small-container{
  max-width: 680px;
}
</style>
