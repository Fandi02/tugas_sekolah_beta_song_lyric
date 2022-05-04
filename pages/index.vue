<template>
  <div class="container-fluid">
    <img src="~/static/4.jpg" alt="" height="450px" width="100%" />
    <div class="input-grup">
      <center>
        <input
          type="text"
          v-model="artist"
          class="input"
          placeholder="Artist"
        />
        <input
          type="text"
          v-model="title"
          class="input"
          placeholder="Title Song"
        />
        <button
          type="button"
          @click="getLyrics()"
          class="button btn btn-primary"
        >
          Search
        </button>
      </center>
    </div>

    <div class="card lirik">
      <div class="card-header">Lyric</div>
      <div class="card-body">
        <h5 class="card-title">Contoh pencarian = Coldplay - Clocks</h5>
        <p class="card-text isi-lirik">
          <pre>
{{ lirik }}
          </pre>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      artist: "",
      title: "",
      lirik: "",
    };
  },
  methods: {
    async getLyrics() {
      await this.$axios
        .get(`v1/${this.artist}/${this.title}`)
        .then((res) => {
          this.lirik = res.data.lyrics;
          console.log(this.lirik);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
.input-grup {
  margin-top: -30px;
}
.input {
  width: 400px;
  height: max-content;
  background-color: white;
  border-radius: 20px;
  padding: 10px;
}
.button {
  border-radius: 20px;
  padding: 10px;
}
.lirik {
  margin: 75px 150px;
}
.isi-lirik {
  font-size: 17px;
  padding: 25px;
}
</style>
