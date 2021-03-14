<template>
  <div>
    <div>
      <h1>Shopping List</h1>
      <div>
        <input v-model="itemInput" type="text" placeholder="Add item here">
        <button @click="addItemToList(itemInput)" class="add_item_button" id="addItemButton">
          {{ addItemButton }}
        </button>
        <div class="item_list">
          <ul>
            <li v-for="item in itemList" :key="item">{{ item }}
              <a href="#" @click="deleteItem(item)" class="delete_item_link" >
                {{ deleteItemLink }}</a>
            </li>
          </ul>
          <div v-show="!isShowDeleteButton">
            <button @click="deleteAllList()" class="delete_all_button">
              {{ deleteAllButton }}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShoppingListComponent',
  data() {
    return {
      itemInput: '',
      addItemButton: 'Add Item',
      deleteAllButton: 'Delete All',
      deleteItemLink: 'Remove',
      itemList: [],
      isShowDeleteButton: true,
      placeHolderText: '',
    };
  },
  mounted() {
    console.info('Dom Mounted.');
    document.addEventListener('keypress', (e) => {
      this.AddItemToListByKeyPress(e);
    });
  },
  updated() {
    console.info('Dom has been updated.');
  },
  methods: {
    /**
     * Handles adding an item to Shopping list front end. Adds item
     * to item list if it does not exist.
     * @param item : item being added to shopping list.
     */
    addItemToList(item) {
      const isItemInlist = this.isItemExist(item);
      if (!isItemInlist && item.toString() !== '') {
        this.itemList.push(item);
        console.info('item added: '.concat(item));
      }
      // removes text from input form on item addition.
      this.itemInput = '';
      this.isShowDeleteButton = this.isEmptyList();
    },
    isEmptyList() {
      return this.itemList.length === 0;
    },
    /**
     * Deletes all items from shopping list array. Deletes all items
     * on shopping list frontend.
     */
    deleteAllList() {
      this.itemList = [];

      // all items are deleted, handles not showing delete all button.
      this.isShowDeleteButton = this.isEmptyList();
      console.info('Items in list have been removed.');
    },
    /**
     * Filters the item being removed from shopping list. Removes item
     * from shopping list array.
     * @param item : item to be removed.
     */
    deleteItem(item) {
      this.itemList = this.itemList.filter((listItem) => listItem !== item);

      // checks if list is empty to handle showing delete all button.
      this.isShowDeleteButton = this.isEmptyList();
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
    /**
     * Handles adding valid item to shopping list on 'enter-key' press.
     * @param e : event handler.
     * @constructor : enter key pressed.
     */
    AddItemToListByKeyPress(e) {
      if (e.keyCode === 13) {
        console.log('enter key pressed, adding item to car if valid');
        this.addItemToList(this.itemInput);
      }
    },
  },
};
</script>

<style>

input[type=text] {
  border-radius: 4px;
  width: 30%;
  margin-right: 5px;
  position: center;
}

.add_item_button {
  border-radius: 4px;
  background-color: darkcyan;
  text-align: center;
  text-decoration: none;
  color: white;
}

.item_list {
}

.delete_item_link {
  color: red;
  text-decoration: none;
}

.delete_all_button {
  border-radius: 4px;
  background-color: red;
  color: white;
}
</style>
