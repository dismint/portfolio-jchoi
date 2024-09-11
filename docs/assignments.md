---
layout: doc
---

<script setup>
  import {data as assignments} from './assignments/assignment.data';
  import { withBase } from 'vitepress';
</script>

# Assignments

<ul v-if="assignments.length > 0">
  <li v-for="assignment of assignments">
    <a :href="withBase(assignment.url)">{{ assignment.frontmatter.title }}</a>
  </li>
</ul>
<p v-else>
  Nothing here yet!
</p>

