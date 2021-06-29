# Задача

`Дано`:
-Ширина ячейки                 ===>  [`cellWidth`]
-Массив со строками(1-5 эл.)   ===>  [`recipientsResult`]

`Задача`:
Написать функцию, которая принимает массив со строками, и возвращает количество элементов, которые поместились.

`Решение`:
 
(Важно не забыть использовать метод filter во второй части решения)
 
Функция должна считать ширину каждого элемента
 
Зная ширину каждого элемента, мы можем добавлять их по очереди, пока их сумма не будет больше чем ширина ячейки
 
Если мы добавили элемент, и разница суммы элементов больше чем ширина ячейки, 
то мы не добавляем этот элемент в результирующий массив, и возвращаем массив со всеми предыдущими элементами


- Функция будет срабатывать внутри метода `onMount`;

##  onMount(()=>{
##    let cellWidth = wrapper.parentElement.offsetWidth;
##    console.log(cellWidth);
##
##    `Здесь будет находится эта функция` 
##
##     getFinalRecipients(cellWidth, recipientsResult)
##
##  });

`Функция которая возвращает склеенную строку из всех элементов массива`
function getString(arrayOfStrings){
    
    return arrayOfStrings.join(",");
  
  };
===================================================//


`Функция которая возвращает длину строки`
  function getTextWidth(text) {
    const canvas = document.createElement("canvas");
    const context = canvas.getContext("2d");
    context.font = "normal 16px arial";
    const metrics = context.measureText(text);
    return metrics.width;
  };
===================================================//



function getFinalRecipients(cellWidth, recipientsResult){
    let result;

    let widthOfElements = recipientsResult.map((el)=>{
        return getTextWidth(el);
    });





    return result;
}



- Примерно так: widthOfElements = [34,56,71]
Надо написать цикл, по массиву widthOfElements, в котором мы будем каждый раз сравнивать ширину ячейки и ширину первого, первого+второго, первого+второго+третьего элементов.