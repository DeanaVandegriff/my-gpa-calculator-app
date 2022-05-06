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
    <div v-for="course in courses" v-bind:key="course.id">
      <h2>Course: {{ course.name }}</h2>
      <h2>Grade: {{ course.grade }}</h2>
    </div>
  </div>
</template>
