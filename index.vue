<template>
    <div class="container-fluid">
      <div class="row my-5">
        <div class="col-lg-6">
          <nuxt-link to="/pengunjung/tambah">
            <div class="card bg-pengunjung rounded-5">
              <div class="card-body">
                <h2>ABSEN MASUK</h2>
              </div>
            </div>
          </nuxt-link>
        </div>
        <div class="col-lg-6">
          <nuxt-link to="/pengunjung">
            <div class="card bg-buku rounded-5">
              <div class="card-body">
                <h2>ABSEN KELUAR</h2>
              </div>
            </div>
          </nuxt-link>
      </div>
    </div>
  </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient();
  const jumlahpengunjung = ref(0);
  const jumlahbuku = ref(0);
  
  async function ambiljumlahpengunjung() {
    const { data, error, count } = await supabase
      .from("pengunjung")
      .select("*", { count: "exact" });
    if (count) jumlahpengunjung.value = count;
  }
  
  async function ambiljumlahbuku() {
    const { data, error, count } = await supabase
      .from("buku")
      .select("*", { count: "exact" });
    if (count) jumlahbuku.value = count;
  }
  
  onMounted(() => {
    ambiljumlahpengunjung();
    ambiljumlahbuku();
  });
  </script>
  
  <style scoped>
  * {
    text-decoration: none;
  }
  .card {
    height: 250px;
    box-shadow: 1px 1px 10px #424242;
  }
  .card.bg-pengunjung {
    margin-top: 5%;
    background-image: url("../assets/img/absen.png");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    
  }
  .card.bg-buku {
    margin-top: 5%;
    background: url("../assets/img/keluar.png");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    
  }
  h2 {
    color: black;
    font: arial;
  }
  h1 {
    color: white;
  }
  .card.bg-warning {
    margin-top: 3%;
  }
  .card.bg-success {
    margin-top: 3%;
  }
  .statistik {
    color: black;
    margin-left: 50px;
  }
  h5 {
    text-align: center;
    margin-top: 80px;
    font-size: 300%;
    color: black;
  }
  h4 {
    text-align: center;
    margin-top: 80px;
    font-size: 300%;
    color: black;
  }
  </style>