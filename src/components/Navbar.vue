<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
const emit = defineEmits(["changePage"]);

function change(page) {
  emit("changePage", page);
}
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow">
    <div class="container-fluid">

      <a class="navbar-brand fw-bold" href="#">
        :briefcase: ModernTech HR System
      </a>

      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav">

        <span class="navbar-toggler-icon"></span>

      </button>

      <div
        class="collapse navbar-collapse"
        id="navbarNav">

        <ul class="navbar-nav ms-auto">

          <li class="nav-item">
            <button
              class="btn btn-dark me-2"
              @click="change('dashboard')">
              Dashboard
            </button>
          </li>

          <li class="nav-item">
            <button
              class="btn btn-dark me-2"
              @click="change('employees')">
              Employees
            </button>
          </li>

          <li class="nav-item">
            <button
              class="btn btn-dark me-2"
              @click="change('payroll')">
              Payroll
            </button>
          </li>

          <li class="nav-item">
            <button
              class="btn btn-dark me-2"
              @click="change('leave')">
              Leave Requests
            </button>
          </li>

          <li class="nav-item">
            <button
              class="btn btn-dark"
              @click="change('attendance')">
              Attendance
            </button>
          </li>

        </ul>

      </div>

    </div>
  </nav>
</template>