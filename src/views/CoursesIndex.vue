<script>
import axios from "axios";

export default {
  data: function () {
    return {
      courses: [],
      point_value: [],
      total: "",
      GPA: "",
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses.json").then((response) => {
      this.courses = response.data;
      console.log("Courses", this.courses);
    });
  },
  methods: {
    calcGPA() {
      var pointTotal = this.courses.map(({ point_value }) => point_value).reduce((a, b) => a + b, 0);
      var creditTotal = this.courses.map(({ credits }) => credits).reduce((a, b) => a + b, 0);
      // this.GPA = Math.round((pointTotal / creditTotal) * 100) / 100;
      this.GPA = (pointTotal / creditTotal).toFixed(2);
    },
  },
};
</script>

<template>
  <div class="index">
    <h1>Courses</h1>
    <button v-on:click="calcGPA()">Cumulative GPA:</button>
    <h2>{{ GPA }}</h2>
    <div class="container">
      <table class="table table-bordered table-striped" id="sortTable">
        <thead class="thead-light">
          <tr>
            <th scope="semester_taken" data-sortable="true">Semester</th>
            <th scope="col" data-sortable="true">Course Name</th>
            <th scope="col" data-sortable="true">Grade</th>
            <!-- <th scope="col">Credits</th>
            <th scope="col">Point Value</th> -->
            <th scope="col" data-sortable="true">More Info</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="course in courses" v-bind:key="course.id">
            <td>{{ course.semester_taken }}</td>
            <td>{{ course.name }}</td>
            <td>{{ course.grade }}</td>
            <!-- <td>{{ course.credits }}</td>
            <td>{{ course.point_value }}</td> -->
            <td><a v-bind:href="`/courses/${course.id}/edit`">More Info!</a></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<style>
.table-striped > tbody > tr:nth-child(odd) > td,
.table-striped > tbody > tr:nth-child(odd) > th {
  background-color: #bed3f0;
}
</style>
