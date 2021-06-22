<script lang="ts">
  export let recipients:Array<string>

  const recipientsResult:Array<string> = recipients; // replace recipients with logic that they want. 

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
<!-- Если к нам пришел массив с длиной больше 1, то надо показать компонент (квадратик с цифрой)  -->
<!-- Если же в ячейку могут поместиться все элементы, то надо показать всех -->
<!-- -->
<!-- -->
<!-- -->
<!-- -->



{#if recipientsResult.length > 1}  
<div class="wrapper">
  <spa class="recipientEmail">{recipientsResult[0]}</spa>
  <span class={"box"}>{`+${recipientsResult.length - 1}`}</span>
</div>


{:else}
<span>{recipientsResult}</span>
{/if}



