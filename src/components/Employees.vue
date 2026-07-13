<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, computed, onMounted } from "vue";
import defaultEmployees from "../data/employees";

const employees = ref([]);

const search = ref("");

const newEmployee = ref({
  name: "",
  department: "",
  position: "",
  salary: ""
});

onMounted(() => {
  const saved = localStorage.getItem("employees");

  if (saved) {
    employees.value = JSON.parse(saved);
  } else {
    employees.value = defaultEmployees;
    saveEmployees();
  }
});

function saveEmployees() {
  localStorage.setItem(
    "employees",
    JSON.stringify(employees.value)
  );
}

function addEmployee() {
  if (
    !newEmployee.value.name ||
    !newEmployee.value.department ||
    !newEmployee.value.position ||
    !newEmployee.value.salary
  ) {
    alert("Please complete all fields.");
    return;
  }

  employees.value.push({
    id: Date.now(),
    name: newEmployee.value.name,
    department: newEmployee.value.department,
    position: newEmployee.value.position,
    salary: Number(newEmployee.value.salary)
  });

  saveEmployees();

  newEmployee.value = {
    name: "",
    department: "",
    position: "",
    salary: ""
  };
}

function deleteEmployee(id) {
  employees.value = employees.value.filter(
    employee => employee.id !== id
  );

  saveEmployees();
}

const filteredEmployees = computed(() => {
  return employees.value.filter(employee =>
    employee.name
      .toLowerCase()
      .includes(search.value.toLowerCase())
  );
});
</script>

<template>

<div class="container">

<h2 class="mb-4">
Employee Management
</h2>

<div class="card mb-4 shadow">

<div class="card-body">

<h5 class="mb-3">
Add Employee
</h5>

<div class="row g-3">

<div class="col-md-3">
<input
v-model="newEmployee.name"
class="form-control"
placeholder="Employee Name">
</div>

<div class="col-md-3">
<input
v-model="newEmployee.department"
class="form-control"
placeholder="Department">
</div>

<div class="col-md-3">
<input
v-model="newEmployee.position"
class="form-control"
placeholder="Position">
</div>

<div class="col-md-2">
<input
v-model="newEmployee.salary"
type="number"
class="form-control"
placeholder="Salary">
</div>

<div class="col-md-1 d-grid">
<button
class="btn btn-success"
@click="addEmployee">
Add
</button>
</div>

</div>

</div>

</div>

<div class="mb-3">

<input
v-model="search"
class="form-control"
placeholder="Search Employee">

</div>

<div class="table-responsive">

<table class="table table-striped table-hover">

<thead class="table-dark">

<tr>

<th>ID</th>

<th>Name</th>

<th>Department</th>

<th>Position</th>

<th>Salary</th>

<th>Action</th>

</tr>

</thead>

<tbody>

<tr
v-for="employee in filteredEmployees"
:key="employee.id">

<td>{{ employee.id }}</td>

<td>{{ employee.name }}</td>

<td>{{ employee.department }}</td>

<td>{{ employee.position }}</td>

<td>R {{ employee.salary.toLocaleString() }}</td>

<td>

<button
class="btn btn-danger btn-sm"
@click="deleteEmployee(employee.id)">

Delete

</button>

</td>

</tr>

</tbody>

</table>

</div>

</div>

</template>