<script lang="ts">
  import { onMount } from 'svelte'

  export let recipients: Array<string>

  const recipientsResult: Array<string> = recipients.map((el)=>` ${el}`) // replace recipients with logic that they want.

  // dom object for recipientEmail wrapper.
  let wrapperNew
  // variable that tells us if text inside wrapperNew was overspilled. (on mounting)
  let isOverlapping

  function isEllipsisActive(e) {
    isOverlapping = e.offsetWidth < e.scrollWidth
  }

  onMount(() => {
    isEllipsisActive(wrapperNew);
    if (isOverlapping && recipientsResult.length > 1) {
      wrapperNew.innerHTML = `${recipientsResult[0]}`;
    };
  });

  console.log(recipientsResult.length)

</script>

<style>
  /* .box {
    color: white;
    padding: 2px 5px;
    font-size: 16px;
    background-color: #666666;
    border-radius: 3px;
    margin-left: 5px;
  }
  .wrapper {
    display: flex;
    justify-content: space-between;
    white-space: nowrap;
    text-overflow: ellipsis;
  } */

  div{
    white-space: nowrap;
    text-overflow: ellipsis;
  }
</style>

<div bind:this="{wrapperNew}">
  <span class="recipientEmail">{recipientsResult}</span>
</div>

<!-- Надо передать в переменную количество успешно отрисованных, не обрезанных емеилов -->