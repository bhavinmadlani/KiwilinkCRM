<template>
  <div v-if="Object.keys(Client).length == 0">
    <v-card v-if="Teasers.length == 0 && !Loading" class="pa-3 grey--text">
      No clients found...
    </v-card>
    <v-card v-for="t in Teasers" :key="t.ID" class="ma-1 pa-3">
      <div class="row">
        <v-icon small>fa-user-circle</v-icon>
        <span>{{ t.Name }}</span>
      </div>
      <div v-if="t.Mobile" class="row">
        <v-icon small>fa-phone-square</v-icon>
        <span>{{ t.Mobile }}</span>
      </div>
      <div v-if="t.Course" class="row">
        <v-icon small>fa-graduation-cap</v-icon>
        <span>{{ t.Course }}</span>
      </div>
      <div v-if="t.Institute" class="row">
        <v-icon small>fa-university</v-icon>
        <span>{{ t.Institute }}</span>
      </div>
      <v-divider></v-divider>
      <v-card-actions class="text-lg-right pb-0">
        <v-btn
          small
          flat
          color="orange lighten-2"
          @click="openClient(t)"
          :loading="t.Loading == true"
        >
          <v-icon size="20">fa-folder-open</v-icon>
          open
        </v-btn>
        <v-spacer></v-spacer>
        <v-btn
          small
          flat
          color="red lighten-2"
          v-if="Employee.IsAdmin"
          @click="deleteClient(t.ID)"
        >
          <v-icon size="20">fa-trash-alt</v-icon>
        </v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  store: ["Teasers", "Client", "Employee", "Loading"],
  methods: {
    openClient(client) {
      this.$store.OpenClient(client);
    },
    deleteClient(id) {
      this.$confirm("Are you sure you want to delete?").then(yes => {
        if (yes) {
          this.$store.DeleteClient(id);
        }
      });
    }
  }
};
</script>

<style scoped>
.v-icon {
  width: 40px;
}
.v-card .row {
  height: 25px;
}
</style>
