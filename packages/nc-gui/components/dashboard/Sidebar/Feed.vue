<script setup lang="ts">
const workspaceStore = useWorkspace()

const { navigateToFeed } = workspaceStore

const { isFeedPageOpened } = storeToRefs(workspaceStore)

const { isNewFeedAvailable } = useProductFeed()

const gotoFeed = () => navigateToFeed()
</script>

<template>
  <NcButton
    v-e="['c:product-feed']"
    type="text"
    full-width
    size="xsmall"
    class="n!xs:hidden my-0.5 w-full !h-7 !rounded-md !font-normal !pl-4.5 !pr-5"
    data-testid="nc-sidebar-product-feed"
    :centered="false"
    :class="{
      '!text-brand-600 !bg-brand-50 !hover:bg-brand-50': isFeedPageOpened,
      '!hover:(bg-gray-200 text-gray-700)': !isFeedPageOpened,
    }"
    @click="gotoFeed"
  >
    <div
      class="flex !w-full items-center gap-2"
      :class="{
        'font-semibold': isFeedPageOpened,
      }"
    >
      <div class="flex flex-1 w-full items-center gap-3">
        <GeneralIcon icon="megaPhone" class="!h-4" />
        <span class="">What’s New!</span>
      </div>
      <div v-if="isNewFeedAvailable" class="w-3 h-3 pulsing-dot bg-nc-fill-red-medium border-2 border-white rounded-full"></div>
    </div>
  </NcButton>
</template>

<style scoped lang="scss">
@keyframes pulse {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.7;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.pulsing-dot {
  animation: pulse 1.5s infinite ease-in-out;
}

:deep(.nc-btn-inner) {
  @apply !w-full;
}
</style>
