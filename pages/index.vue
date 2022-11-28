<template>
  <div>
    <client-only>
      <artwork></artwork>
    </client-only>
    <client-only>
      <space></space>
    </client-only>
  </div>
</template>
<script>
import artwork from "../components/Artwork/xmas.vue"
import space from "../components/Artwork/space.vue"

export default {
  components: {
    artwork,
    space,
  }
}
</script>

