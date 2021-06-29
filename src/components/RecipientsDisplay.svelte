<script lang="ts">
  import { onMount } from 'svelte'

  export let recipients: Array<string>;

  const recipientsResult: Array<string> = recipients;

  function getTextWidth(text) {
    const canvas = document.createElement("canvas");
    const context = canvas.getContext("2d");
    context.font = "normal 16px arial";
    const metrics = context.measureText(text);
    return metrics.width;
  };
  
  // Надо написать функцию которая принимает массив, а возвращает строку всех элементов.

  function getString(arrayOfStrings){
    let result;
    result = arrayOfStrings.join(",");
    return result;
  };
  
  let stringFromArray = getString(recipientsResult);
  // Надо переписать функцию, надо вытащить ширину каджого элемента в массиве, а потом сложить их.

  let wrapper;
  
  onMount(()=>{
    let cellWidth = wrapper.parentElement.offsetWidth;
    console.log(cellWidth);
    

  });

</script>




<span bind:this="{wrapper}" class="recipientEmail">{recipientsResult}</span>





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
  }

  div{
    white-space: nowrap;
    text-overflow: ellipsis;
  } */
</style>