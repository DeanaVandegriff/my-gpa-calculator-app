<script>
import axios from "axios";

export default {
  data: function () {
    return {
      courses: [],
      point_value: [],
      total: "",
      GPA: "",
      name: "",
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses.json").then((response) => {
      this.courses = response.data;
      console.log("Courses", this.courses);
    });
    this.getUserName();
  },
  methods: {
    calcGPA() {
      var pointTotal = this.courses.map(({ point_value }) => point_value).reduce((a, b) => a + b, 0);
      var creditTotal = this.courses.map(({ credits }) => credits).reduce((a, b) => a + b, 0);
      this.GPA = (pointTotal / creditTotal).toFixed(2);
    },
    getUserName() {
      const userName = localStorage.getItem("name");
      this.name = userName;
    },
  },
};
</script>

<template>
  <div class="index">
    <h1>{{ this.name }}'s Courses</h1>
    <button v-on:click="calcGPA()">Cumulative GPA:</button>
    <h2>{{ GPA }}</h2>
    <div class="container">
      <table class="table table-bordered table-striped">
        <thead class="thead-light">
          <tr>
            <th scope="semester_taken">Semester</th>
            <th scope="col">Course Name</th>
            <th scope="col">Grade</th>
            <th scope="col">More Info</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="course in courses" v-bind:key="course.id">
            <td>{{ course.semester_taken }}</td>
            <td>{{ course.name }}</td>
            <td>{{ course.grade }}</td>
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
