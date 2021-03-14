<template>
  <div class="container">
    <h1>Shopping List</h1>
    <div class="wrap">
      <input v-model="itemInput" type="text" placeholder="Items to add" />
      <button @click="addItemToList(itemInput)" class="add_item_button">
        {{ addItemButton }}
      </button>
      <div class="item_list">
        <ul>
          <li v-for="item in itemList" :key="item">
            {{ item }}
            <a href="#" @click="deleteItem(item)" class="delete_item_link">
              {{ deleteItemLink }}</a
            >
          </li>
        </ul>
        <div v-show="!isEmptyList">
          <button @click="deleteAllList()" class="delete_all_button">
            {{ deleteAllButton }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShoppingListComponent",
  data() {
    return {
      itemInput: "",
      addItemButton: "Add Item",
      deleteAllButton: "Delete All",
      deleteItemLink: "Remove",
      itemList: [],
      isEmptyList: true,
    };
  },
  mounted() {
    console.info("Dom Mounted.");
  },
  updated() {
    console.info("Dom has been updated.");
  },
  methods: {
    /**
     * Handles adding an item to Shopping list front end. Adds item
     * to item list if it does not exist.
     * @param item : item being added to shopping list.
     */
    addItemToList(item) {
      const isItemInlist = this.isItemExist(item);
      if (!isItemInlist) {
        this.itemList.push(item);
        console.info("item added: ".concat(item));
      }
      this.isEmptyList = false;
    },
    /**
     * Deletes all items from shopping list array. Deletes all items
     * on shopping list frontend.
     */
    deleteAllList() {
      this.itemList = [];

      // all items are deleted, handles not showing delete all button.
      this.isEmptyList = true;
      console.info("Items in list have been removed.");
    },
    /**
     * Filters the item being removed from shopping list. Removes item
     * from shopping list array.
     * @param item : item to be removed.
     */
    deleteItem(item) {
      this.itemList = this.itemList.filter((listItem) => listItem !== item);

      // checks if list is empty to handle showing delete all button.
      if (this.itemList.length === 0) {
        this.isEmptyList = true;
      }
    },
    /**
     * Handles checking if an item exists before storing it into shopping list.
     * If item exists, does nothing.
     * @param item : item being checked in list.
     * @returns {boolean}
     */
    isItemExist(item) {
      for (let i = 0; i < this.itemList.length; i += 1) {
        if (this.itemList[i] === item) {
          return true;
        }
      }
      return false;
    },
  },
};
</script>

<style>
.container {
  margin-top: 20em;
}

h1 {
  float: left;
  margin-left: 35.5vw;
}

.wrap {
  margin-left: 35vw;
  margin-right: 35vw;
}

input[type="text"] {
  border-radius: 4px;
  height: 2.25em;
  width: 25vw;
  margin-right: 5px;
  position: center;
}

.add_item_button {
  border-radius: 20%;
  padding: 0.5em;
  background-color: navy;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  color: white;
}

.item_list {
  margin-top: 1em;
  margin-left: 0.5vw;
  padding-top: 1.5em;
  padding-bottom: 1.5em;
  width: 28vw;
  border: 1.5px lightgrey solid;
  position: center;
  text-decoration: none;
}

.delete_item_link {
  border-radius: 20%;
  padding: 0.5em;
  color: red;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
}

.delete_all_button {
  border-radius: 4px;
  background-color: red;
  color: white;
}
</style>
