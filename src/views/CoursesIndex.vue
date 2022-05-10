<script>
import axios from "axios";

export default {
  data: function () {
    return {
      courses: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses.json").then((response) => {
      this.courses = response.data;
      console.log("Courses", this.courses);
    });
  },
};
</script>

<template>
  <div class="index">
    <h1>Courses</h1>

    <!-- <div v-for="course in courses" v-bind:key="course.id">
      <h2>Course: {{ course.name }}</h2>
      <h2>Grade: {{ course.grade }}</h2>
    </div> -->
    <div class="container">
      <table class="table table-bordered">
        <thead class="thead-light">
          <tr>
            <th scope="col">Course Name</th>
            <th scope="col">Grade</th>
            <th scope="col">More Info</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="course in courses" v-bind:key="course.id">
            <td>{{ course.name }}</td>
            <td>{{ course.grade }}</td>
            <td><a v-bind:href="`/courses/${course.id}/edit`">More Info!</a></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
