<script lang="ts">
  import { onMount } from 'svelte'

  export let recipients: Array<string>

  const recipientsResult: Array<string> = recipients

  function getTextWidth(text) {
    const canvas = document.createElement('canvas')
    const context = canvas.getContext('2d')
    context.font = 'normal 16px arial'
    const metrics = context.measureText(text)
    return metrics.width
  }

  function getString(arrayOfStrings) {
    return arrayOfStrings.join(',')
  }

  let stringFromArray = getString(recipientsResult)
  

  let wrapper
  let numberComponent

  // =================================================================||
  // =================================================================||
  // =================================================================||

  function getTruncatedValues() {
    let cellWidth = wrapper.parentElement.offsetWidth - 61 // 61 px (Ширина компонента с цифрой с отступами)

    function getFinalRecipients(cellWidth, recipientsResult) {
      let widthOfElements = recipientsResult.map((el, i) => {
        if (i > 0) {
          return getTextWidth(el) + 4.4453125
        } else {
          return getTextWidth(el)
        }
      })

      function merge(textArr, widthArr) {
        const result = []
        for (let i = 0; i < textArr.length; i++) {
          result.push({
            text: textArr[i],
            width: widthArr[i],
          })
        }
        return result
      }

      let arrayOfObjects = merge(recipientsResult, widthOfElements)
      let resultArr = []
      let widthSum = 0
      arrayOfObjects.map(el => {
        widthSum += el.width
        if (cellWidth > widthSum) {
          resultArr.push(el.text)
        }
      })

      if (resultArr.length === 0) {
        resultArr.push(arrayOfObjects[0].text)
      }

      wrapper.innerHTML = resultArr.map(el => ` ${el}`) + ', ...'
      let restNumber = arrayOfObjects.length - resultArr.length
      numberComponent = restNumber
    }

    getFinalRecipients(cellWidth, recipientsResult)
  }

  onMount(() => {
    getTruncatedValues()
  })

  window.addEventListener('resize', () => {
    getTruncatedValues()
  })
  // есть проблема, когда делаю ресайз - остается 「, ...」 в тех местах где изначально был только 1 элемент.
</script>

<style>
  .box {
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

  div {
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .recipientEmail {
    text-overflow: ellipsis;
    overflow: hidden;
  }
</style>

{#if numberComponent === 0}
  <span bind:this={wrapper} class="recipientEmail">
    {recipientsResult.map(el => ` ${el}`)}
  </span>
{:else}
  <div class="wrapper">
    <span bind:this={wrapper} class="recipientEmail">{recipientsResult}</span>
    <span class="box">{`+${numberComponent}`}</span>
  </div>
{/if}
