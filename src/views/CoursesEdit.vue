<script>
import axios from "axios";

export default {
  data: function () {
    return {
      course: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/courses/" + this.$route.params.id + ".json").then((response) => {
      console.log(response.data);
      this.course = response.data;
    });
  },
  methods: {
    updateCourse: function () {
      console.log("Update a course!");
      axios.patch("http://localhost:3000/courses/" + this.$route.params.id, this.course).then((response) => {
        console.log("Success", response.data);
        this.$router.push("/courses");
      });
    },
    destroyCourse: function (course) {
      axios.delete("http://localhost:3000/courses/" + course.id).then((response) => {
        console.log("course removed", response);
        this.$router.push("/courses");
      });
    },
  },
};
</script>

<template>
  <div class="courses-edit">
    <form v-on:submit.prevent="updateCourse()">
      <h1>Update a Course</h1>
      <div>
        <div class="form-group">
          Name:
          <input type="text" v-model="course.name" />
        </div>
        <div class="form-group">
          Grade:
          <input type="text" v-model="course.grade" />
        </div>
        <div class="form-group">
          Credits:
          <input type="text" v-model="course.credits" />
        </div>
        <div class="form-group">
          Semester:
          <input type="text" v-model="course.level" />
        </div>
        <div class="form-group">
          Semester:
          <input type="text" v-model="course.semester_taken" />
        </div>
      </div>
      <input type="submit" value="Update Course" />
    </form>
    <br />
    <button v-on:click="destroyCourse(course)">Delete Course</button>
    <br />
    <br />
    <a href="/courses">Back to all Courses</a>
  </div>
</template>
