<template>
  <div>
    <div class="container" v-if="icon">
      <img :src="getImage" alt="Chuck" />
      <div>
        <p>{{ quote }}</p>
        <span>{{ date }}</span>
      </div>
    </div>
    <div class="container" v-else>
      <img
        src="https://shortpixel.com/img/spinner2.gif"
        alt="loading"
      />Loading...
    </div>
  </div>
</template>

<script>
const URL = "https://api.chucknorris.io/jokes/random";
export default {
  name: "NorrisJoke",
  created() {
    this.fetchApi();
  },
  computed: {
    getImage() {
      return this.type === "chuck"
        ? this.icon
        : "https://pbs.twimg.com/profile_images/3681800067/52aca11437c84b556072673c70480174.jpeg";
    }
  },
  props: {
    type: {
      type: String,
      default: "chuck",
      required: false,
      validator: v => ["nicolas", "chuck"].includes(v)
    }
  },
  data() {
    return {
      icon: "",
      quote: "",
      date: ""
    };
  },
  methods: {
    fetchApi() {
      fetch(URL)
        .then(res => res.json())
        .then(data => {
          this.icon = data.icon_url;
          this.quote = data.value;
          this.date = data.updated_at;
        });
    }
  }
};
</script>

<style>
.container {
  display: inline-flex;
  max-width: 500px;
  border: 1px solid #999;
  padding: 5px;
  padding-right: 20px;
  border-radius: 10px;
  font-family: "Montserrat";
  background: #eee;
}
.container > div {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
img {
  width: 60px;
  height: 60px;
  margin-right: 10px;
}
p {
  margin: 0;
}
time {
  font-family: Arial;
  font-size: 12px;
  color: purple;
}
</style>
