<script setup>
import { ref } from "vue";

const leaveRequests = ref([]);

const form = ref({
  employee: "",
  type: "",
  start: "",
  end: ""
});

function submitRequest() {

  if (
    !form.value.employee ||
    !form.value.type ||
    !form.value.start ||
    !form.value.end
  ) {
    alert("Please complete all fields.");
    return;
  }

  leaveRequests.value.push({
    id: Date.now(),
    employee: form.value.employee,
    type: form.value.type,
    start: form.value.start,
    end: form.value.end,
    status: "Pending"
  });

  form.value = {
    employee: "",
    type: "",
    start: "",
    end: ""
  };
}

function approve(request){
  request.status = "Approved";
}

function decline(request){
  request.status = "Declined";
}
</script>

<template>

<div class="container">

<h2 class="mb-4">
Leave Requests
</h2>

<div class="card shadow mb-4">

<div class="card-body">

<div class="row g-3">

<div class="col-md-3">
<input
class="form-control"
v-model="form.employee"
placeholder="Employee Name">
</div>

<div class="col-md-3">

<select
class="form-select"
v-model="form.type">

<option disabled value="">
Leave Type
</option>

<option>Annual Leave</option>

<option>Sick Leave</option>

<option>Family Responsibility</option>

</select>

</div>

<div class="col-md-2">
<input
type="date"
class="form-control"
v-model="form.start">
</div>

<div class="col-md-2">
<input
type="date"
class="form-control"
v-model="form.end">
</div>

<div class="col-md-2 d-grid">

<button
class="btn btn-success"
@click="submitRequest">

Submit

</button>

</div>

</div>

</div>

</div>

<table class="table table-striped">

<thead class="table-dark">

<tr>

<th>Employee</th>

<th>Type</th>

<th>Start</th>

<th>End</th>

<th>Status</th>

<th>Actions</th>

</tr>

</thead>

<tbody>

<tr
v-for="request in leaveRequests"
:key="request.id">

<td>{{ request.employee }}</td>

<td>{{ request.type }}</td>

<td>{{ request.start }}</td>

<td>{{ request.end }}</td>

<td>

<span
class="badge bg-warning"
v-if="request.status==='Pending'">

Pending

</span>

<span
class="badge bg-success"
v-if="request.status==='Approved'">

Approved

</span>

<span
class="badge bg-danger"
v-if="request.status==='Declined'">

Declined

</span>

</td>

<td>

<button
class="btn btn-success btn-sm me-2"
@click="approve(request)">

Approve

</button>

<button
class="btn btn-danger btn-sm"
@click="decline(request)">

Decline

</button>

</td>

</tr>

</tbody>

</table>

</div>

</template>