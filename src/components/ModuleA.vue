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
            <h3 class="headline mb-0">Module A</h3>
            <h4 class="subtitle-1">Post a new message</h4>
          </div>
        </v-card-title>

        <v-card-text>
          <form>
            <v-text-field
              v-model="newMessage"
              label="Message"
              required
            />
            <v-btn
              class="mr-4"
              @click="submit"
            >Post</v-btn>
          </form>
        </v-card-text>
      </v-card>
    </v-hover>

  </v-container>
</template>
<script>
export default {
  name: "ModuleA",
  props: {},
  data() {
    return {
      newMessage: ""
    };
  },
  methods: {
    submit: function() {
      let instance = this,
        message = this.newMessage,
        user = localStorage.getItem("user"),
        token = localStorage.getItem("token");
      this.axios
        .post(`/messages/${user}`, {
          token: token,
          message: message,
          time: Date.now()
        })
        .then(response => {
          console.log(response);
          if (response.status == 200) {
            instance.$router.go()
          }
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>



