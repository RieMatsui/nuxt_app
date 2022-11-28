<template>
  <div>
    <no-ssr>
      <artwork></artwork>
    </no-ssr>
    <no-ssr>
      <space></space>
    </no-ssr>
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

