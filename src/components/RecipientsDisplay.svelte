<script lang="ts">
  import { onMount } from 'svelte';
  export let recipients:Array<string>

  const recipientsResult:Array<string> = recipients; // replace recipients with logic that they want. 
  
  let wrapperNew;

  function isEllipsisActive(e) {
     console.log(e.offsetWidth < e.scrollWidth);
    };

  onMount(() => {
    isEllipsisActive(wrapperNew);
  });

  
</script>

<style>
  .box{
    color: white;
    padding: 2px 5px;
    font-size: 16px;
    background-color: #666666;
    border-radius: 3px;
    margin-left:5px ;
  }
  .wrapper{
    display: flex;
    justify-content: space-between;
  }

  .recipientEmail{
  }

</style>


{#if recipientsResult.length > 1}  
<div bind:this="{wrapperNew}" class="wrapper">
  <span class="recipientEmail">{recipientsResult[0]}</span>
  <span class="box">{`+${recipientsResult.length - 1}`}</span>
</div>


{:else}
<span bind:this="{wrapperNew}">{recipientsResult}</span>
{/if}



