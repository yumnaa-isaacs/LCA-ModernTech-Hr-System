<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref } from "vue";

const attendance = ref([
  {
    id: 1,
    employee: "John Smith",
    date: "2026-06-26",
    status: "Present"
  },
  {
    id: 2,
    employee: "Sarah Johnson",
    date: "2026-06-26",
    status: "Absent"
  },
  {
    id: 3,
    employee: "Michael Brown",
    date: "2026-06-26",
    status: "On Leave"
  }
]);

const form = ref({
  employee: "",
  date: "",
  status: "Present"
});

function addAttendance() {

  if(
    !form.value.employee ||
    !form.value.date
  ){
    alert("Please complete all fields.");
    return;
  }

  attendance.value.push({
    id: Date.now(),
    employee: form.value.employee,
    date: form.value.date,
    status: form.value.status
  });

  form.value = {
    employee:"",
    date:"",
    status:"Present"
  };
}

function removeAttendance(id){
  attendance.value = attendance.value.filter(
    record => record.id !== id
  );
}
</script>

<template>

<div class="container">

<h2 class="mb-4">
Attendance
</h2>

<div class="card shadow mb-4">

<div class="card-body">

<div class="row g-3">

<div class="col-md-4">
<input
class="form-control"
v-model="form.employee"
placeholder="Employee Name">
</div>

<div class="col-md-3">
<input
type="date"
class="form-control"
v-model="form.date">
</div>

<div class="col-md-3">

<select
class="form-select"
v-model="form.status">

<option>Present</option>
<option>Absent</option>
<option>On Leave</option>

</select>

</div>

<div class="col-md-2 d-grid">

<button
class="btn btn-primary"
@click="addAttendance">

Add

</button>

</div>

</div>

</div>

</div>

<table class="table table-hover">

<thead class="table-dark">

<tr>

<th>Employee</th>

<th>Date</th>

<th>Status</th>

<th>Action</th>

</tr>

</thead>

<tbody>

<tr
v-for="record in attendance"
:key="record.id">

<td>{{ record.employee }}</td>

<td>{{ record.date }}</td>

<td>

<span
class="badge bg-success"
v-if="record.status==='Present'">

Present

</span>

<span
class="badge bg-danger"
v-if="record.status==='Absent'">

Absent

</span>

<span
class="badge bg-warning text-dark"
v-if="record.status==='On Leave'">

On Leave

</span>

</td>

<td>

<button
class="btn btn-danger btn-sm"
@click="removeAttendance(record.id)">

Delete

</button>

</td>

</tr>

</tbody>

</table>

</div>

</template>