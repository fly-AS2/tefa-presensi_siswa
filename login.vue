<template>
    <div class="container-fluid mt-5">
      <div class="row justify-content-center">
        <div class="col-md-6">
          <nuxt-link to="/pages/index">
          <h2>Login</h2>
          <form @submit.prevent="Login">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input 
                type="email" 
                class="form-control" 
                id="email" 
                v-model="email" 
                required 
              />
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input 
                type="password" 
                class="form-control" 
                id="password" 
                v-model="password" 
                required 
              />
            </div>
            <button 
              type="submit" 
              class="btn btn-primary" 
              :disabled="loading"
            >
              <span v-if="loading">Loading...</span>
              <span v-else>Login</span>
            </button>
            <div v-if="error" class="alert alert-danger mt-3">
              {{ error }}
            </div>
          </form>
          </nuxt-link>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient();
  const email = ref("");
  const password = ref("");
  const loading = ref(false);
  const error = ref(""); 
  
  const Login = async () => {
    loading.value = true;
    error.value = "";
    const { data, error: loginError } = await supabase.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    });
    
    if (data) {
      loading.value = false
      navigateTo('/pages/index')
    }
  };
  </script>
  