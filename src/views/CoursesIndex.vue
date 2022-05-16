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
      var total = this.courses.map(({ point_value }) => point_value).reduce((a, b) => a + b, 0);
      this.GPA = Math.round((total / this.courses.length) * 100) / 100;
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
      <table class="table table-bordered">
        <thead class="thead-light">
          <tr>
            <th scope="col">Course Name</th>
            <th scope="col">Grade</th>
            <th scope="col">Point Value</th>
            <th scope="col">More Info</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="course in courses" v-bind:key="course.id">
            <td>{{ course.name }}</td>
            <td>{{ course.grade }}</td>
            <td>{{ course.point_value }}</td>
            <td><a v-bind:href="`/courses/${course.id}/edit`">More Info!</a></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
