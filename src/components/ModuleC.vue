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
            <h3 class="headline mb-0">Module C</h3>
            <h4 class="subtitle-1">Message History</h4>
          </div>
        </v-card-title>

        <v-card-text>
           <v-btn
              class="mr-4"
              @click="view"
            >Click to view</v-btn>
        </v-card-text>
      </v-card>
    </v-hover>
  </v-container>
</template>
<script>
export default {
  name: "ModuleC",
  props: {},
  methods: {
    view: function() {
      let username = localStorage.getItem('user')
      this.$router.push(`/history/${username}`)
    }
  }
};
</script>