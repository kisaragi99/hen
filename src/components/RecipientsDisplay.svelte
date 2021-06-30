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
    let fullArrayWidth = getTextWidth(stringFromArray);

    function getFinalRecipients(cellWidth, recipientsResult){ 
      let widthOfElements = recipientsResult.map((el, i)=>{
        if(i > 0){
          return getTextWidth(el) + 4.4453125;
        } else{
          return getTextWidth(el);
        }
      });


      for(let [i, el] of widthOfElements.entries()){
        // Здесь надо проверять входят ли все элементы в ячейку?
        // Зная ширину каждого элемента, мы можем добавлять их по очереди, пока их сумма не будет больше чем ширина ячейки
        // Если мы добавили элемент, и разница суммы элементов больше чем ширина ячейки, 
        // то мы не добавляем этот элемент в результирующий массив, и возвращаем массив со всеми предыдущими элементами

      };


    };

    getFinalRecipients(cellWidth, recipientsResult);

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