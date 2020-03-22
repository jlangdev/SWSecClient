<template>
  <v-container>
    <v-hover>
      <v-card
        slot-scope="{ hover }"
        :class="`elevation-${hover ? 8 : 2} clickable`"
      >
        <v-card-title
          primary-title
          size="100%"
        >
          <div>
            <h3 class="headline mb-0">Module B</h3>
            <h4 class="subtitle-1">Latest Message</h4>
          </div>
        </v-card-title>

        <v-card-text>
          <span v-html="newestMessage"></span>
        </v-card-text>
      </v-card>
    </v-hover>
  </v-container>

</template>
<script>
export default {
  name: "ModuleB",
  props: {},
  data(){
    return{
      newestMessage: '',
    }
  },
  methods: {
    clicked: function() {}
  },
  mounted() {
    let instance = this, 
      user = localStorage.getItem("user"),
      token = localStorage.getItem("token");
    this.axios
      .get(`/messages/${user}/new`, {
        headers: { "x-access-token": token }
      })
      .then(response => {
        console.log(response);
        if (response.status == 200) {
          instance.newestMessage = `<blockquote class="blockquote">${response.data.response.message}</blockquote>`
        }
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>