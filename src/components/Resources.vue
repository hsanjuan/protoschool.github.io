<template>
  <div data-cy='resources-content' class='lesson-text lh-copy mb4'>
    <p>
      Ready to learn more? There are plenty of additional resources to explore, both in ProtoSchool and beyond.
      <span v-if='data.length > 1'>Here are some of our favorites:</span>
      <span v-else>Here's our top pick:</span>
    </p>
    <div v-for='(item, idx) in data' :key='`resources-${idx}`' class='mb3'>
      <p class='ma0 flex items-center'>
        <a class='b blue link' :href='item.link' target='_blank'>{{item.title}}</a>
        <span class='ml2 ph2 bg-navy br-pill white f7'>{{item.type}}</span>
        <span
          v-if='item.link.includes("/proto.school/")'
          class='ml2 ph2 bg-aqua br-pill white f7'
        >ProtoSchool</span>
      </p>
      <div v-if='item.description' class='ma0 resource-desc' v-html='parse(item.description)'></div>
    </div>
    <FeedbackSurvey class="mv4" />
    <NewsletterSubscription class="mv4" />
  </div>
</template>

<script>
import marked from 'marked'

import NewsletterSubscription from './forms/NewsletterSubscription.vue'
import FeedbackSurvey from './forms/feedback-survey/FeedbackSurvey.vue'

export default {
  components: {
    NewsletterSubscription,
    FeedbackSurvey
  },
  props: {
    data: Array
  },
  methods: {
    parse (description) {
      return marked(description || '')
    }
  }
}
</script>

<style>
.resource-desc > p {
  margin-top: 0;
}
</style>
