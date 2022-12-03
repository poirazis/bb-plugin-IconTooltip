<script>
  import { getContext } from "svelte"

  export let icon
  export let size
  export let color
  export let tooltip
  export let delay
  export let duration
  export let position
  export let type
  export let onClick

  const { styleable } = getContext("sdk")
  const component = getContext("component")

  $: $component.styles = {
    ...$component.styles,
    normal: {
      ...$component.styles.normal,
      color: color || "var(--spectrum-global-color-gray-900)",
    },
  }
</script>

<div use:styleable={$component.styles}>
  {#if icon}     
     <span class="u-tooltip-showOnHover" style="margin: 0px 0px; cursor: default;">
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <i class="{icon} {size}" on:click={onClick} class:hoverable={onClick != null}/> 
      {#if tooltip}
         <!-- content here -->
      
      <div
      style="--delay:{delay}ms; --duration:{duration}ms;" 
      class="spectrum-Tooltip spectrum-Tooltip--{position} spectrum-Tooltip--{type}">
        <span class="spectrum-Tooltip-label">{tooltip}</span>
        <span class="spectrum-Tooltip-tip"></span>
      </div>
      {/if}
    </span>
  {/if}
</div>

<style>
  .u-tooltip-showOnHover .spectrum-Tooltip{
    transition-property: all !important;
    transition-duration: var(--duration) !important;
    transition-delay: var(--delay) !important;
    overflow-wrap: break-word !important;
    min-width: 160px !important;
    white-space: normal !important;
    word-wrap: normal !important;
    z-index: 9999 !important;
    text-align: center !important;
  }

  @media (hover: hover) {
    .hoverable:hover {
      color: var(--spectrum-alias-icon-color-selected-hover) !important;
      cursor: pointer;
    }
  }
  .hoverable:active {
    color: var(--spectrum-alias-icon-color-selected-hover) !important;
  }
</style>