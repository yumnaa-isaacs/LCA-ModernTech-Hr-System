<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, computed, onMounted } from "vue";
import defaultEmployees from "../data/employees";

const employees = ref([]);

onMounted(() => {
  const saved = localStorage.getItem("employees");

  if (saved) {
    employees.value = JSON.parse(saved);
  } else {
    employees.value = defaultEmployees;
  }
});

const totalEmployees = computed(() => employees.value.length);

const totalPayroll = computed(() =>
  employees.value.reduce((sum, emp) => sum + emp.salary, 0)
);

const averageSalary = computed(() =>
  employees.value.length
    ? Math.round(totalPayroll.value / employees.value.length)
    : 0
);

const departments = computed(() => {
  return [...new Set(employees.value.map(emp => emp.department))].length;
});
</script>

<template>
  <div class="container">

    <h2 class="mb-4">
      HR Dashboard
    </h2>

    <div class="row g-4">

      <div class="col-md-3">
        <div class="card bg-primary text-white shadow">
          <div class="card-body text-center">
            <h5>Total Employees</h5>
            <h2>{{ totalEmployees }}</h2>
          </div>
        </div>
      </div>

      <div class="col-md-3">
        <div class="card bg-success text-white shadow">
          <div class="card-body text-center">
            <h5>Monthly Payroll</h5>
            <h4>R {{ totalPayroll.toLocaleString() }}</h4>
          </div>
        </div>
      </div>

      <div class="col-md-3">
        <div class="card bg-warning text-dark shadow">
          <div class="card-body text-center">
            <h5>Average Salary</h5>
            <h4>R {{ averageSalary.toLocaleString() }}</h4>
          </div>
        </div>
      </div>

      <div class="col-md-3">
        <div class="card bg-info text-white shadow">
          <div class="card-body text-center">
            <h5>Departments</h5>
            <h2>{{ departments }}</h2>
          </div>
        </div>
      </div>

    </div>

    <div class="card mt-5 shadow">

      <div class="card-body">

        <h4>Company Overview</h4>

        <p>
          Welcome to the ModernTech Solutions HR Management System.
          This application allows HR staff to manage employee records,
          payroll, attendance and leave requests in one place.
        </p>

      </div>

    </div>

  </div>
</template>