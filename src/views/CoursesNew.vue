<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newCoursesParams: {},
      errors: [],
    };
  },
  methods: {
    createCourse: function () {
      console.log("Enter a Course");
      axios
        .post("http://localhost:3000/courses.json", this.newCoursesParams)
        .then((response) => {
          console.log("course entered", response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
<template>
  <div class="courses-new">
    <form v-on:submit.prevent="createCourse()">
      <h1>Enter a Course</h1>
      <div class="course-group">
        Course Name:
        <input class="form-control-mx-auto" style="width: 200px" type="text" v-model="newCoursesParams.name" />
      </div>
      <div class="course-group">
        Grade:
        <select class="custom-select" style="width: 200px" v-model="newCoursesParams.grade">
          <option selected>grade</option>
          <option>A+</option>
          <option>A</option>
          <option>A-</option>
          <option>B+</option>
          <option>B</option>
          <option>B-</option>
          <option>C+</option>
          <option>C</option>
          <option>C-</option>
          <option>D+</option>
          <option>D</option>
          <option>D-</option>
          <option>F</option>
        </select>
      </div>
      <div class="course-group">
        Credits:
        <select class="custom-select" style="width: 200px" v-model="newCoursesParams.credits">
          <option selected>credits</option>
          <option>0.5</option>
          <option>1</option>
        </select>
      </div>
      <div class="course-group">
        Level:
        <select class="custom-select" style="width: 200px" v-model="newCoursesParams.level">
          <option selected>levels</option>
          <option>traditional</option>
          <option>honors</option>
          <option>AP</option>
        </select>
      </div>
      <div class="course-group">
        Semester:
        <select class="custom-select" style="width: 200px" v-model="newCoursesParams.semester_taken">
          <option selected>semester</option>
          <option>9th Grade: Semester One</option>
          <option>9th Grade: Semester Two</option>
          <option>10th Grade: Semester One</option>
          <option>10th Grade: Semester Two</option>
          <option>11th Grade: Semester One</option>
          <option>11th Grade: Semester Two</option>
          <option>12th Grade: Semester One</option>
          <option>12th Grade: Semester Two</option>
        </select>
      </div>
      <br />
      <input type="submit" value="Create Course" />
    </form>
  </div>
</template>

<style>
.container-fluid {
  padding-left: 30%;
}
</style>
