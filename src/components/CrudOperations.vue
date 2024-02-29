<template>
  <div>
    <v-form @submit.prevent="addItem">
      <v-container>
        <v-row>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="inputText"
              label="Enter something..."
              solo
              clearable
            ></v-text-field>
            <v-btn @click="addItem" color="primary">Submit</v-btn>
          </v-col>
          <v-col cols="12">
            <v-btn @click="sortByAlphabet">Sort Alphabetically</v-btn>
            <ul>
              <li v-for="(item, index) in items" :key="index">
                <span @click="editItem(item)" style="margin-right: 10px">{{ item }}</span>
                <v-icon small class="mr-2" @click="editItemDialog(item)"> mdi-pencil </v-icon>
                <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
              </li>
            </ul>
          </v-col>
        </v-row>
      </v-container>
    </v-form>

    <v-dialog v-model="editDialog" max-width="500">
      <v-card>
        <v-card-title>Edit Item</v-card-title>
        <v-card-text>
          <v-text-field v-model="editedItem" label="Edit item"></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="saveEdit">Save</v-btn>
          <v-btn color="error" @click="closeEditDialog">Cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: "",
      items: [],
      editDialog: false,
      editedItem: "",
      editedItemIndex: null,
    };
  },
  methods: {
    addItem() {
      if (this.inputText.trim() !== "") {
        this.items.push(this.inputText);
        this.inputText = "";
      }
    },
    editItem(item) {
      this.editedItem = item;
      this.editedItemIndex = this.items.indexOf(item);
      this.editDialog = true;
    },
    editItemDialog(item) {
      this.editedItem = item;
      this.editedItemIndex = this.items.indexOf(item);
      this.editDialog = true;
    },
    saveEdit() {
      if (this.editedItem.trim() !== "") {
        this.$set(this.items, this.editedItemIndex, this.editedItem);
        this.closeEditDialog();
      }
    },
    closeEditDialog() {
      this.editDialog = false;
      this.editedItem = "";
      this.editedItemIndex = null;
    },
    deleteItem(item) {
      const index = this.items.indexOf(item);
      if (index !== -1) {
        this.items.splice(index, 1);
      }
    },
    sortByAlphabet() {
      this.items.sort();
    },
  },
};
</script>

