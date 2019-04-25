<template>
  <v-container>
    <v-card>
      <v-card-title class="grey lighten-2 pb-0">Search</v-card-title>
      <v-form lazy-validation>
        <v-layout ma-2 row wrap justify-start>
          <v-flex xs12 md5 pa-1>
            <v-text-field label="ID" v-model="searchItem.id" :counter="10" clearable/>
          </v-flex>
          <v-flex xs12 md5 pa-1>
            <v-text-field label="Name" v-model="searchItem.name" :counter="20" clearable/>
          </v-flex>
          <v-flex xs12 md2 align-self-center>
            <v-card-actions class="justify-center">
              <v-btn round small color="primary" @click="search()">
                <v-icon>search</v-icon>SEARCH
              </v-btn>
            </v-card-actions>
          </v-flex>
        </v-layout>
      </v-form>
    </v-card>
    <v-card>
      <v-card-title class="grey lighten-2 pb-0">Result</v-card-title>
      <transition name="fade">
        <v-dialog v-model="dialog" max-width="640px" persistent>
          <v-card>
            <v-card-title class="headline grey lighten-2">Office Profile</v-card-title>
            <v-card-text>
              <small>* required field</small>
              <v-container grid-list-md>
                <v-layout wrap>
                  <v-flex xs12 md6>
                    <v-text-field label="ID" v-model="editedItem.id" disabled></v-text-field>
                  </v-flex>
                  <v-flex md6></v-flex>
                  <v-flex xs12 md6>
                    <v-text-field
                      label="Name"
                      v-model="editedItem.name"
                      clearable
                      required
                      :disabled="op == 'd'"
                    ></v-text-field>
                  </v-flex>
                  <v-flex md6></v-flex>
                  <v-flex xs12 md6>
                    <v-text-field
                      label="Zipcode"
                      v-model="editedItem.zipcode"
                      clearable
                      required
                      :disabled="op == 'd'"
                    ></v-text-field>
                  </v-flex>
                  <v-flex md6></v-flex>
                  <v-flex xs12 md6>
                    <v-text-field
                      label="Address"
                      v-model="editedItem.address"
                      clearable
                      required
                      :disabled="op == 'd'"
                    ></v-text-field>
                  </v-flex>
                </v-layout>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="gray darken-1" flat @click="cancel()">Cancel</v-btn>
              <v-btn color="primary darken-1" flat @click="saveItem()" v-show="op != 'd'">Save</v-btn>
              <v-btn color="error darken-1" flat @click="removeItem()" v-show="op == 'd'">Remove</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </transition>
      <v-data-table class="elevation-1 ma-4" :headers="headers" :items="offices">
        <template v-slot:items="props">
          <template v-for="n in (headers.length - 1)">
            <td
              :class="'text-xs-' + headers[n - 1].align"
              style="white-space: nowrap"
              v-text="props.item[headers[n - 1].value]"
            ></td>
          </template>
          <td class="text-xs-center" xs1>
            <v-btn flat small fab @click="edit(props.item)">
              <v-icon>edit</v-icon>
            </v-btn>
            <v-btn flat small fab @click="remove(props.item)">
              <v-icon>delete</v-icon>
            </v-btn>
          </td>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    searchItem: {
      id: "",
      name: ""
    },

    headers: [
      { text: "ID", align: "left", sortable: true, value: "id" },
      { text: "Name", align: "left", sortable: true, value: "name" },
      { text: "Zipcode", align: "left", sortable: true, value: "zipcode" },
      { text: "Address", align: "left", sortable: true, value: "address" },
      { text: "Actions", align: "center", sortable: false }
    ],
    offices: [],

    dialog: false,
    op: "",
    editedIndex: -1,
    editedItem: {
      id: "",
      name: ""
    }
  }),
  methods: {
    edit(item) {
      this.open(item, "u");
    },
    remove(item) {
      this.open(item, "d");
    },
    open(item, op) {
      this.editedIndex = this.offices.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.op = op;
      this.dialog = true;
    },
    search() {
      this.offices = [
        { id: "0001", name: "Office1", zipcode: "1000001", address: "東京都千代田区千代田"},
        { id: "0002", name: "Office2", zipcode: "1000001", address: "東京都千代田区千代田"},
        { id: "0003", name: "Office3", zipcode: "1000001", address: "東京都千代田区千代田"},
        { id: "0004", name: "Office4", zipcode: "1000001", address: "東京都千代田区千代田"},
      ];
    },
    cancel() {
      this.dialog = false;
    },
    saveItem() {
      if (this.editedIndex > -1) {
        Object.assign(this.offices[this.editedIndex], this.editedItem);
      } else {
        this.offices.push(this.editedItem);
      }
      this.dialog = false;
    },
    removeItem() {
      confirm("Are you sure you want to remove this group?") &&
        this.groups.splice(this.editedIndex, 1);
      this.dialog = false;
    }
  }
};
</script>
