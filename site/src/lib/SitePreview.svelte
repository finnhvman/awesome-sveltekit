<script lang="ts">
  import Icon from '@iconify/svelte'
  import { Screenshot } from '.'
  import { filter_tags } from './stores'
  import type { Site } from './types'

  export let site: Site
  export let idx = 0
  export let tags = false
</script>

<a href={site.slug}>
  <Screenshot title={site.title} resolution=".small" style="cursor: pointer;" />
</a>
<div class="flex">
  <span>
    {idx > 0 ? `${idx}. ` : ``}<a href={site.url}>{site.title}</a>
  </span>
  {#if site.repo_stars}
    <small class="flex">
      <Icon icon="octicon:star" />
      &nbsp;{site.repo_stars.toLocaleString()}
    </small>
  {/if}
</div>
{#if tags}
  <p class="tags flex">
    <Icon icon="octicon:tag" style="margin: 0 1ex 0 0;" />
    {#each site.tags as tag}
      <small class:active={$filter_tags.find((t) => t.label === tag)}>
        {tag}
      </small>
    {/each}
  </p>
{/if}

<style>
  div.flex {
    margin-top: 6pt;
    justify-content: space-between;
  }
  p.tags small {
    background-color: rgba(255, 255, 255, 0.2);
    line-height: 1.2em;
    padding: 1pt 3pt;
    margin: 3pt 0;
    border-radius: 3pt;
    font-size: 9pt;
  }
  p.tags small:not(:last-child) {
    margin-right: 1ex;
  }
  p.tags small.active {
    font-weight: bold;
  }
</style>
