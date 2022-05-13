<script>
import axios from "axios";

export default {
  data: function () {
    return {
      courses: [],
      point_value: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses.json").then((response) => {
      this.courses = response.data;
      this.point_value = response.data[0].point_value;
      console.log("Courses", this.courses, "Point Values", this.point_value);
    });
  },
  // methods: {
  //   pointSum() {
  //     return this.courses.map(({ point_value }) => point_value).reduce((a, b) => a + b, 0);
  //   },
  // },
};
</script>

<template>
  <div class="index">
    <h1>Courses</h1>
    <button v-on:click="pointSum()">Total Points:</button>
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
