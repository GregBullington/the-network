<template>
  <div class="row justify-content-center">
    <div class="col mx-5">
      <form @submit.prevent = "search" class="input-group" >
        <input type="text" v-model="searchText" class="form-control" placeholder="Search posts...">
      </form>
    </div>
  </div>
</template>


<script>
import { ref } from "@vue/reactivity"
import { allPostsService } from "../services/AllPostsService"
import { profileService } from "../services/ProfileService"
import { logger } from "../utils/Logger"
import Pop from "../utils/Pop"
export default {
  setup(){
    const searchText = ref("")
    return {
      async search() {
        try {
          await allPostsService.getAllPosts("?query=" + searchText.value)
          // await profileService.getAllProfiles("?query=" + searchText.value)
        } catch (error) {
          logger.error(error)
          Pop.toast(error.message, "error")
        }
      },
      searchText,
    }
  }
}
</script>


<style lang="scss" scoped>

</style>