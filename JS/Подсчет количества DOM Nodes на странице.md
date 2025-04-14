```js
// Функция для подсчета всех типов узлов в документе
function countAllNodeTypes() {
    const nodeCounts = {
        ELEMENT_NODE: 0,
        ATTRIBUTE_NODE: 0,
        TEXT_NODE: 0,
        COMMENT_NODE: 0,
        DOCUMENT_NODE: 0,
        DOCUMENT_TYPE_NODE: 0,
        DOCUMENT_FRAGMENT_NODE: 0
    };

    // Рекурсивная функция для обхода узлов
    function traverseNodes(node) {
        switch (node.nodeType) {
            case Node.ELEMENT_NODE:
                nodeCounts.ELEMENT_NODE++;
                break;
            case Node.ATTRIBUTE_NODE:
                nodeCounts.ATTRIBUTE_NODE++;
                break;
            case Node.TEXT_NODE:
                nodeCounts.TEXT_NODE++;
                break;
            case Node.COMMENT_NODE:
                nodeCounts.COMMENT_NODE++;
                break;
            case Node.DOCUMENT_NODE:
                nodeCounts.DOCUMENT_NODE++;
                break;
            case Node.DOCUMENT_TYPE_NODE:
                nodeCounts.DOCUMENT_TYPE_NODE++;
                break;
            case Node.DOCUMENT_FRAGMENT_NODE:
                nodeCounts.DOCUMENT_FRAGMENT_NODE++;
                break;
        }

        // Обход дочерних узлов
        node.childNodes.forEach(traverseNodes);
    }

    // Начинаем с корневого узла документа
    traverseNodes(document);

    return nodeCounts;
}

// Получаем и выводим количество узлов
const counts = countAllNodeTypes();
// Сортировка по значениям
const sortedObj = Object.fromEntries(
    Object.entries(counts).sort(([, valueA], [, valueB]) => valueB - valueA)
);
// Суммирование всех значений
const totalSum = Object.values(sortedObj).reduce((accumulator, currentValue) => accumulator + currentValue, 0);

console.log('Количество узлов', totalSum, JSON.stringify(sortedObj));

```

#js/снипеты  #performance 