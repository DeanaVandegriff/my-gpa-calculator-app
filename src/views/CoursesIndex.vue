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
    <h1>Zach Morris' Courses</h1>

    <!-- <div v-for="course in courses" v-bind:key="course.id">
      <h2>Course: {{ course.name }}</h2>
      <h2>Grade: {{ course.grade }}</h2>
    </div> -->
    <table class="table table-bordered">
      <thead class="thead-light">
        <tr>
          <th scope="col" sortable="semester_taken">Semester</th>
          <th scope="col">Course Name</th>
          <th scope="col">Grade</th>
          <th scope="col">Credits</th>
          <th scope="col">Level</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="course in courses" v-bind:key="course.id">
          <td>{{ course.semester_taken }}</td>
          <td>{{ course.name }}</td>
          <td>{{ course.grade }}</td>
          <td>{{ course.credits }}</td>
          <td>{{ course.level }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
