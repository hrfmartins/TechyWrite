<template>
  <ul class="gap-4 mx-auto mb-5">
    <li
      v-for="opportunity in opportunitiesData"
      :key="opportunity.link"
      class="p-3 w-full h-full"
    >
      <div class="shadow-lg hover:shadow-xl">
        <div
          class="flex rounded-lg h-full bg-gray-800 bg-opacity-30 p-8 flex-col hover:bg-opacity-50 "
          style="position: relative"
        >
          <h2 class="flex rounded-2xl opportunity-type text-xs font-semibold mr-2 px-2.5 py-0.5 dark:bg-green-700 dark:text-green-100 rounded-lg">
            {{ opportunity.type }}
          </h2>
          <div class="flex items-center mb-3 justify" style="white-space: normal; width: 70%;">
            <a
              class="text-2xl font-semibold text-white"
              :href="opportunity.link"
              target="_blank"
              rel="noopener"
              >{{ opportunity.name }}</a
            >
          </div>
          <div class="flex justify-start mb-2 mt-4" v-if="opportunity.description">
            <em class="bi bi-info-circle me-3 icon"></em>
            <h3 class="text-white" style="margin-top: 3px">
              {{ opportunity.description }}
            </h3>
          </div>

          <div class="flex justify-start mb-2" v-if="opportunity.contact">
            <em class="bi bi-envelope me-3 icon"></em>
            <a :href="'mailto:' + opportunity.contact"
              ><h3 class="text-white" style="margin-top: 3px; word-break: break-all;">
                {{ opportunity.contact }}
              </h3></a
            >
          </div>

          <hr
            v-if="
              opportunity.description &&
              (opportunity.maxRate ||
                opportunity.hourlyMaxRate ||
                opportunity.royaltyRate)
            "
            style="margin-bottom: 5px"
          />

          <div
            v-if="
              opportunity.maxRate ||
              opportunity.hourlyMaxRate ||
              opportunity.royaltyRate
            "
            class="flex justify-start mb-2"
          >
            <em class="bi bi-credit-card icon"></em>
            <h3
              class="text-white"
              style="margin-top: 3px"
              v-if="opportunity.minRate && opportunity.maxRate"
            >
              ${{ opportunity.minRate }} - ${{ opportunity.maxRate }}
            </h3>
            <h3
              class="text-white"
              style="margin-top: 3px"
              v-if="!opportunity.minRate && opportunity.maxRate"
            >
              ${{ opportunity.maxRate }}
            </h3>
            <h3
              class="text-white"
              style="margin-top: 3px"
              v-if="opportunity.hourlyMaxRate"
            >
              ${{ opportunity.hourlyMaxRate }} per hour
            </h3>
            <h3
              class="text-white"
              style="margin-top: 3px"
              v-if="opportunity.royaltyRate"
            >
              {{ opportunity.royaltyRate }}
            </h3>
            
          </div>
          <div
              class="flex opportunity-category justify-content-end flex-wrap"
            >
              <li v-for="i in opportunity.categories" v-bind:key="i">
                <span
                  class="bg-green-900 text-green-100 text-xs font-semibold mr-2 px-2.5 py-0.5 dark:bg-green-700 dark:text-green-100 flex rounded-lg mt-2"
                  >{{ i }}</span
                >
              </li>
            </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    opportunitiesData: {
      type: Array,
      required: true,
    },
  },
};
</script>
