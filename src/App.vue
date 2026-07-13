<script setup>
import { ref } from "vue";

import Navbar from "./components/Navbar.vue";
import Dashboard from "./components/Dashboard.vue";
import Employees from "./components/Employees.vue";
import Payroll from "./components/Payroll.vue";
import LeaveRequests from "./components/LeaveRequests.vue";
import Attendance from "./components/Attendance.vue";

const currentPage = ref("dashboard");
</script>

<template>

<Navbar
@changePage="currentPage = $event"/>

<div class="container py-4">

<Dashboard
v-if="currentPage==='dashboard'"/>

<Employees
v-if="currentPage==='employees'"/>

<Payroll
v-if="currentPage==='payroll'"/>

<LeaveRequests
v-if="currentPage==='leave'"/>

<Attendance
v-if="currentPage==='attendance'"/>

</div>

</template>