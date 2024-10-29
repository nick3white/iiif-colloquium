<script>
let { active, invert = false } = $props()
</script>
<div class="wrapper" class:invert on:click={() => active = !active} class:active>
  <div class="icon">
    <svg  viewBox="0 0 24 24">
      <g>
        <path d="M11 6h2v11h-2z" />
        <path d="m12 18.414-4.707-4.707 1.414-1.414L12 15.586l3.293-3.293 1.414 1.414L12 18.414z" />
      </g>
    </svg>
  </div>
</div>
<style>
.active {
  opacity: 0 !important;
}
.invert {
  transform: rotate(180deg);
  top: 50px;
}
.wrapper:not(.invert){
  bottom: 0;

}
.wrapper {
  position: absolute;
  z-index: 10;
  lefT: 0;
  right: 0;

  padding-block: 0 16px;
  display: flex;
  justify-content: center;
}
.icon {
  pointer-events: auto;
  width: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 200ms;
  border: 8px solid transparent;
  animation: bounce 1s infinite;
  & svg {

    fill: var(--foreground);
  }
}
.icon:hover {
  border: 8px solid var(--background);
  & svg {
    fill: var(--background);
  }
}

</style>
