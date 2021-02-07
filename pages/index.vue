<template>
  <div>
    <v-btn color="primary" fixed right top fab elevation="24">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-container grid-list-xs>
      <h1 class="display-2 mb-4">Documents</h1>
      <v-card>
        <v-card-title primary-title>
          <v-text-field v-model="search" label="Search" append-icon="mdi-magnify" @keyup="getDoc()"></v-text-field>
        </v-card-title>
        <v-data-table :headers="headers" :items="docs" hide-default-footer>
        </v-data-table>
      </v-card>
      <v-pagination
        class="ma-4"
        :length="totlaPage"
        v-model="page"
        total-visible="7"
        @input="getDoc()"
      ></v-pagination>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      page: 1,
      totlaPage: 0,
      limit: 5,
      docs: [],
      search: '',
      headers: [
        { text: "ID", value: "id" },
        { text: "Title", value: "title" },
        { text: "Description", value: "description" },
        { text: "Create", value: "created_at" }
      ]
    };
  },
  mounted() {
    this.getDoc();
  },
  methods: {
    async getDoc() {
      let offset = (this.page - 1) * this.limit;
      let rs = await this.$axios.get("doc", {
        params: {
          limit: this.limit,
          offset: this.search ? 0 : offset,
          search: this.search
        }
      });

      let { data } = rs;
      this.docs = data.docs;
      this.totlaPage = Math.ceil(data.count_all / this.limit);
      console.log(rs);
    }
  }
};
</script>

<style></style>
