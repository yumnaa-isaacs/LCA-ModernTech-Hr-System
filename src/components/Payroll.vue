<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, computed, onMounted } from "vue";
import defaultEmployees from "../data/employees";

const employees = ref([]);
const selectedEmployee = ref(null);

onMounted(() => {
  const saved = localStorage.getItem("employees");

  if (saved) {
    employees.value = JSON.parse(saved);
  } else {
    employees.value = defaultEmployees;
  }
});

const totalPayroll = computed(() => {
  return employees.value.reduce(
    (total, employee) => total + employee.salary,
    0
  );
});

function generatePayslip(employee) {
  selectedEmployee.value = employee;
}
</script>

<template>

<div class="container">

<h2 class="mb-4">
Payroll
</h2>

<div class="alert alert-primary">

<h4>
Monthly Payroll:
<strong>
R {{ totalPayroll.toLocaleString() }}
</strong>
</h4>

</div>

<div class="table-responsive">

<table class="table table-bordered table-hover">

<thead class="table-dark">

<tr>

<th>Name</th>

<th>Monthly Salary</th>

<th>Annual Salary</th>

<th>Payslip</th>

</tr>

</thead>

<tbody>

<tr
v-for="employee in employees"
:key="employee.id">

<td>{{ employee.name }}</td>

<td>R {{ employee.salary.toLocaleString() }}</td>

<td>
R {{ (employee.salary * 12).toLocaleString() }}
</td>

<td>

<button
class="btn btn-primary btn-sm"
@click="generatePayslip(employee)"
data-bs-toggle="modal"
data-bs-target="#payslipModal">

Generate

</button>

</td>

</tr>

</tbody>

</table>

</div>

<div
class="modal fade"
id="payslipModal"
tabindex="-1">

<div class="modal-dialog">

<div class="modal-content">

<div class="modal-header">

<h5 class="modal-title">

Digital Payslip

</h5>

<button
class="btn-close"
data-bs-dismiss="modal">

</button>

</div>

<div
class="modal-body"
v-if="selectedEmployee">

<h4>{{ selectedEmployee.name }}</h4>

<hr>

<p>
Department:
<strong>
{{ selectedEmployee.department }}
</strong>
</p>

<p>
Position:
<strong>
{{ selectedEmployee.position }}
</strong>
</p>

<p>
Monthly Salary:
<strong>
R {{ selectedEmployee.salary.toLocaleString() }}
</strong>
</p>

<p>
Annual Salary:
<strong>
R {{ (selectedEmployee.salary*12).toLocaleString() }}
</strong>
</p>

</div>

<div class="modal-footer">

<button
class="btn btn-secondary"
data-bs-dismiss="modal">

Close

</button>

</div>

</div>

</div>

</div>

</div>

</template>