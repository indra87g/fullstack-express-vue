<script setup>
import { reactive, ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
import api from "../../services/api";
const user = reactive({
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
});
const validation = ref([]);
const register = async () => {
  await api
    .post("/api/register", {
      name: user.name,
      email: user.email,
      password: user.password,
    })
    .then(() => {
      router.push({
        name: "login",
      });
    })
    .catch((error) => {
      validation.value = error.response.data;
    });
};
</script>

<template>
  <div class="row justify-content-center">
    <div class="row justify-content-center">
      <div class="col-md-5">
        <div class="card border-0 rounded shadow-sm">
          <div class="card-body">
            <h4>REGISTER</h4>
            <hr />
            <div v-if="validation.errors" class="mt-2 alert alert-danger">
              <ul class="mt-0 mb-0">
                <li v-for="(error, index) in validation.errors" :key="index">
                  {{ `${error.path} : ${error.msg}` }}
                </li>
              </ul>
            </div>
            <form @submit.prevent="register">
              <div class="row">
                <div class="col-md-12 mb-3">
                  <div class="form-group">
                    <label class="mb-1 fw-bold">Full Name</label>
                    <input
                      type="text"
                      v-model="user.name"
                      class="form-control"
                      placeholder="Full Name"
                    />
                  </div>
                </div>
              </div>

              <div class="row">
                <div class="col-md-6 mb-3">
                  <div class="form-group">
                    <label class="mb-1 fw-bold">Email address</label>
                    <input
                      type="email"
                      v-model="user.email"
                      class="form-control"
                      placeholder="Email Address"
                    />
                  </div>
                </div>
                <div class="col-md-6 mb-3">
                  <div class="form-group">
                    <label class="mb-1 fw-bold">Password</label>
                    <input
                      type="password"
                      v-model="user.password"
                      class="form-control"
                      placeholder="Password"
                    />
                  </div>
                </div>
              </div>
              <button type="submit" class="btn btn-primary w-100">
                REGISTER
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
