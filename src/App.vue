<template>
  <div>
    <header>Bookmark App</header>
    <!-- COMPONENT -->
      <AddingNewBookmark
      :bookmark="bookmark"
      :updateStatus="updateStatus"
      @save-data="saveData"
      @update-data="updateData"
      @cancel-update="cancelUpdate"
      />
    <!-- /COMPONENT -->

      <TheBookMarkContainer
          :bookmarkList="bookmarkList"
          :bookmark="bookmark"
          :showInputArea="showInputArea"
          @update-item="updateItem"
          @delete-data="deleteData"
      />

  </div>
</template>

<script>
import axios from "axios";
import AddingNewBookmark from "@/components/AddingNewBookmark"
import TheBookMarkContainer from "@/components/TheBookMarkContainer"
export default {
  components:{
    AddingNewBookmark,
    TheBookMarkContainer
  },
  data() {
    return {
      bookmarkList: [],
      bookmark: {
        title: null,
        description: null,
        url: null
      },
      updateID: null,
      updateStatus: false,
      showInputArea:false
    };
  },
  methods: {
    saveData() {
      axios.post("http://localhost:3000/bookmarks", this.bookmark).then(bookmark_save_response => {
        console.log("bookmark_save_response", bookmark_save_response);
        // Created...
        if (bookmark_save_response.status === 201) {
          this.bookmarkList.push(bookmark_save_response.data);
        }

        this.bookmark = {
          title: null,
          description: null,
          url: null
        };
      });
    },
    deleteData(id) {
      axios.delete(`http://localhost:3000/bookmarks/${id}`).then(bookmark_delete_response => {
        console.log("bookmark_delete_response", bookmark_delete_response);
        this.bookmarkList = this.bookmarkList.filter(b => b.id !== id);
      });
    },
    updateData() {
      axios.patch(`http://localhost:3000/bookmarks/${this.updateID}`, this.bookmark).then(update_response => {
        const matchedBookmark = this.bookmarkList.findIndex(b => b.id === this.updateID);
        if (matchedBookmark > -1) {
          this.bookmarkList[matchedBookmark] = {
            ...this.bookmark
          };

          this.updateStatus = false;
          this.updateID = null;
          this.bookmark = {
            title: null,
            description: null,
            url: null
          };
        }
      });
    },
    updateItem(bookmarkItem) {
      console.log("bookmark", bookmarkItem);
      // this.bookmark = bookmarkItem;
      this.bookmark = {
        id:bookmarkItem.id,
        title: bookmarkItem.title,
        description: bookmarkItem.description,
        url: bookmarkItem.url
      };
      // this.bookmark = {
      //   ...bookmarkItem
      // };
      this.showInputArea= true;
      this.updateID = bookmarkItem.id;
      this.updateStatus = true;

    },
    cancelUpdate() {
      this.updateStatus = false;
      this.bookmark = {
        title: null,
        description: null,
        url: null
      };
    }

  },
  created() {
    axios
        .get("http://localhost:3000/bookmarks")
        .then(bookmark_response => {
          console.log("bookmark_response ", bookmark_response);
          this.bookmarkList = bookmark_response.data;
        })
        .catch(e => {
          console.log("Error", e);
        });
  }
};
</script>

<style scoped>
.form-container {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
