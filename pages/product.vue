<template>
<main>
    <navbar/>
      <div class="jumbotron">
        <h1>product</h1>
      </div>
  <div class="container">
    <div>
        <div class="row">
          <div class="col-md-12">
            <div v-if="loading" class="text-center">
              <img src="~/static/assets/loading1.gif" alt="">
            </div>
          </div>

          <div class="col-md-4" v-for="item in items" :key="item.id">
            <div class="card mb-3">
              <div class="card-header">
                <img :src="item.foto" width="100%"> 
              </div>
              <div class="card-body">
                <h4>{{ item.nama }}</h4>
                <h4>Rp{{ item.harga }}</h4>
                <a :href="item.link_eksternal" class="btn btn-danger btn-block">Beli Via Wa</a>
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>
  <footer id="sticky-footer" class="flex-shrink-0 py-4 bg-dark text-white-50">
          <div class="container text-center">
            <small>&copy; 2022 Copyright, RAFIQ STORE</small>
          </div>
        </footer>
</main>
</template>

<script>
export default {
  data() {
    return {
      items: '',
      loading: true,
    }
  },
  mounted() {
    this.ambilData()
  },
  methods: {
    async ambilData() {
      const { data, error } = await this.$supabase
        .from('tb_produk')
        .select()
      if(data) 
        this.items = data
        this.loading = false
      if(error) console.log(error)
    }
  }
}
</script>
