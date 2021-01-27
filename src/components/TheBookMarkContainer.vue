<template>
  <!-- COMPONENT -->
  <div class="container">
    <div class="bookmark--app--container">
      <!-- COMPONENT -->
      <TheBookmarkItem
          v-for="bookmarkItem in bookmarkList"
          :key="bookmarkItem.id"
          :bookmarkItem="bookmarkItem"
          :bookmarkList="bookmarkList"
          :showInputArea="showInputArea"
          :bookmark="bookmark"
          @update-item="$emit('update-item', $event)"
          @delete-data="$emit('delete-data', $event)"
      />
      <!-- /COMPONENT -->
    </div>
  </div>
  <!-- /COMPONENT -->
</template>
<script>
import TheBookmarkItem from "./TheBookmarkItem";

export default {
  components:{
    TheBookmarkItem
  },
  props:["bookmarkList","bookmark","showInputArea"],
  emits:['delete-data','update-item'],

}
</script>
