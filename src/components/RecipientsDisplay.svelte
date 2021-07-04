<script lang="ts">
  import { onMount } from 'svelte'

  export let recipients: Array<string>

  let wrapper: {
    parentElement: { offsetWidth: number }
    innerHTML: string | string[]
  }

  let numberComponent: number

  // array that contains width of recipients array elements.
  let widthOfElements: Array<number> = recipients.map((el, i) => {
    if (i > 0) {
      return getTextWidth(el) + 4.4453125
    } else {
      return getTextWidth(el)
    }
  })

  // function that accepts string and returns its width
  function getTextWidth(text: string): number {
    const canvas = document.createElement('canvas')
    const context = canvas.getContext('2d')
    context.font = 'normal 16px arial'
    const metrics = context.measureText(text)
    return metrics.width
  }

  // function that merges two arrays into one array of objects
  function merge(textArr: Array<string>, widthArr: Array<number>) {
    const result = []
    for (let i = 0; i < textArr.length; i++) {
      result.push({
        text: textArr[i],
        width: widthArr[i],
      })
    }
    return result
  }
  // this function checks if recipients fit into cell of a table by comparing width and then changes innerHTML of wrapper object
  function getFinalRecipients(cellWidth: number, recipients: any[]): void {
    let arrayOfObjects = merge(recipients, widthOfElements)
    let resultArr: Array<object> = []
    let widthSum: number = 0

    for (let el of arrayOfObjects) {
      widthSum += el.width
      if (cellWidth >= widthSum) {
        resultArr.push(el.text)
      }
    }

    if (resultArr.length === 0) {
      resultArr.push(arrayOfObjects[0].text)
    }

    let restNumber = arrayOfObjects.length - resultArr.length

    numberComponent = restNumber

    wrapper.innerHTML =
      restNumber >= 1
        ? resultArr.map(el => ` ${el}`) + ', ...'
        : resultArr.map(el => ` ${el}`)
  }

  function getTruncatedValues(): void {
    let cellWidth = wrapper.parentElement.offsetWidth - 54
    getFinalRecipients(cellWidth, recipients)
  }

  onMount(() => {
    getTruncatedValues()
  })
</script>

<style>
  .box {
    color: white;
    padding: 2px 5px;
    font-size: 16px;
    background-color: #666666;
    border-radius: 3px;
  }
  .wrapper {
    display: flex;
    justify-content: space-between;
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
    {recipients.map(el => ` ${el}`)}
  </span>
{:else}
  <div class="wrapper">
    <span bind:this={wrapper} class="recipientEmail">{recipients}</span>
    <span class="box">{`+${numberComponent}`}</span>
  </div>
{/if}
