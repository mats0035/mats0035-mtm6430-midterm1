<template>
  <div class="testimonial">
    <h1>Testimonials</h1>
    <!-- <MakeTestimonial :testimonialList="testimonialList"/> -->
    <div class="testimonial-container">
      <div v-for="list in testimonialList" class="testimonial-box">
        <p>{{ list.name }} - {{ list.position }}</p>
        <p>{{ list.comment }}</p>
      </div>
      <!-- <span>{{ iterate() }}</span> -->
    </div>
    <div>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" @submit.prevent="submitForm('ruleForm')">
        <el-form-item prop="name">
          <el-input v-model="ruleForm.name" placeholder="Your Name"></el-input>
        </el-form-item>
        <el-form-item prop="position">
          <el-input v-model="ruleForm.position" placeholder="Position Title"></el-input>
        </el-form-item>
        <el-form-item prop="comment">
          <el-input type="textarea" v-model="ruleForm.comment" placeholder="Your Comments"></el-input>
        </el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">Submit</el-button>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      testimonialList: [],
      ruleForm: {
        name: "",
        position: "",
        comment: ""
      },
      rules: {
        name: [
          {
            required: true,
            message: "First ame is required",
            trigger: "blur"
          }
        ],
        position: [
          {
            required: true,
            message: "Last Name is required",
            trigger: "blur"
          }
        ],
        comment: [
          {
            required: true,
            message: "This field is required",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    submitForm(formName) {
      // Check if all the required fields are filled, and show a modal
      // If not, show errors under the unfilled fields
      this.$refs[formName].validate(valid => {
        if (valid) {
          const obj = {
            'name' : this.ruleForm.name,
            'position' : this.ruleForm.position,
            'comment' : this.ruleForm.comment
          };
          this.testimonialList.push(obj);
        } else {
          return false;
        }
      });
    }
  }
}
</script>

<style>
  .testimonial {
    max-width: 800px;
    margin: auto;
    text-align: left;
    padding-top: 100px;
    padding-bottom: 70px;
  }
.dialog-container {
  display: flex;
  margin: auto 20px;
  text-align: left;
}

.testimonial-container {
  display: flex;
  flex-wrap: wrap;
}
.testimonial-box {
  flex: 0 calc(50% - 40px);
  margin: 5px;
  padding: 10px;
  background-color: #e0daff;
}
</style>
