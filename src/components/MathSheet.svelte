<style>

    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
    }

    /* Firefox */
    input[type=number] {
    -moz-appearance: textfield;
    }
    div.page {   
        background-color: antiquewhite;
        height: 100vh;
    }
    div.worksheet {   
        padding-top: 2%;
        width: 100%;
        display: grid;
        grid-template-columns: 25% auto 25%;
        column-gap: 15px;
    }
    div.container {   
        width: 100%;
        display: grid;
        grid-template-columns: auto 412px 25px 412px auto;
        row-gap: 5px;
    }
    div.count {
        font-size: x-large;
    }
    div.numberRow {
        border: 1px solid gray;
        padding: 10px;
        min-width: 263px;
    }
    div.onesRow {
        display: grid;
        grid-template-columns: 30px 30px 30px 30px 30px;
        grid-template-rows: 30px 30px;
        gap: 50px;
        row-gap: 25px;
        padding: 30px;
        padding-top: 10px;
        padding-bottom: 10px;
        height: 100%;
    }
    div.tensRow {
        display: flex;
        flex-direction: row-reverse;
        flex-wrap: wrap;
        gap: 10px;
        min-width: 412px;
        max-width: 412px;
        min-height: 204px
    }

    button.onesElement, button.onesElement:focus {
        height: 30px;
        max-height: 30px;
        width: 30px;
        text-align: center;
        outline: none;
        border: 1px solid gray;
    }
    button.tensElement, button.tensElement:focus {
        width: 30px;
        height: 182px;
        text-align: right;
        padding: 0;
        outline: none;
        border: 1px solid gray;
    }
    div.tenOnes {
        width: 30px;
        margin: 0;
        padding:0;
        height: 100%;
    }
    div.oneInTenElement, div.oneInTenElement:focus {
        height: 15px;
        max-height:15px;
        width: 15px;
        text-align: center;
    }
    div.oneInTenElement:first-child {
        border-top: 0px solid;
    }
    div.oneInTenElement {
        display: block;
        height: 18px;
        max-height: 18px;
        width: 28px;
        text-align: center;
        line-height: 1;
        border-top: 1px solid;
    }
    button.addElement {
        vertical-align: center;
    }
    .invisible {
        display: none;
    }

    span.warn {
        color: darkred;
    }
    div.disabled {
        pointer-events: none;
        opacity: 0.4;
    }
    button {
        user-select: none;
    }
    .equation {
        display: grid;
        grid-template-columns: auto 45px 45px auto;
        grid-template-rows: 45px 45px 45px;
        grid-gap: 10px;
        font-size: xx-large;
        margin-top: 30%;
        text-align: center;
    }
    button.onesToTen {
        margin-right: -4px;
        height: 182px;
        border: 1px solid gray;
        margin-top: 10px;
    }
    div.addOnes {
        display: flex;
        align-content: flex-start;
        flex-direction: row;    
        padding: 10px;
    }
    div.addTens {
        display: flex;
        align-content: flex-start;
        flex-direction: row-reverse;
        padding: 10px;
    }
    .middleAction {
        margin-top: -100px;
        margin-bottom: -100px;
        z-index: 10;
    }
    input.number1 {
        background-color: rgb(178, 241, 178);
        grid-column: 3;
        max-width: 45px;
        text-align: right;
    }

    input.number2 {
        background-color: rgb(150, 182, 230);
        grid-column: 3;
        max-width: 45px;
        text-align: right;
    }

    input.resultNumber {
        grid-column: 3;
        max-width: 45px;
        text-align: right;
        background-color: rgb(255, 255, 0); 
    }

    select.operation {
        grid-column: 2;
        max-width: 45px;
    }
    div.equals {
        grid-column: 2;
        max-width: 45px;
    }
    .noDrop {
        background-color: coral;
    }
    div.firstTensElements, div.firstOnesElements {
        background-color: rgb(178, 241, 178);
    }
    div.secondTensElements, div.secondOnesElements {
        background-color: rgb(150, 182, 230);
    }
    button.onesElement {
        background-color: rgb(255, 255, 0);
    }
    button.tensElement {
        background-color: rgb(255, 255, 0); 
    }
    button.crossedOut {
        background-color: rgb(150, 182, 230);
    }
</style>
<div class="page">
    <div class="worksheet">
        <div>
            <button on:click={reset}>Reset</button>
            <div class="equation">
                <div/>
                <input class="number1" type="number"  bind:value={number1}/>
                <select class="operation" bind:value={operation}>
                    <option value="+">+</option>
                    <option value="-">-</option>
                </select>
                <input class="number2" type="number" bind:value={number2}/>
                <div class="equals">=</div>
                <input class="resultNumber" type="number"/>
            </div>
        </div>
        <div class="container">
            <div/><h3>Tens</h3><div/><h3>Ones</h3><div/>
            <div/>
            <div class="numberRow tensRow firstTensElements" class:disabled={firstTensItems.disabled}>
                {#each firstTensItems.elements as item}
                    <button class="tensElement" on:pointerdown={startDragRemoveFirstTen}>
                        <div class="tenOnes">
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                        </div>
                    </button>
                {/each}
            </div>
            <div class=""><button class="onesToTen" on:pointerdown={startDragMoveTenOnesToOneTen} class:invisible={uncheckedOnesItemsCount<10}>{"<"}</button></div>
            <div class="numberRow onesRow firstOnesElements" class:disabled={firstOnesItems.disabled}>
                {#each firstOnesItems.elements as item}
                    <button class="onesElement removeElement {item.crossedOut ? "crossedOut" : ""}" on:click={() => item = clicked(item)} on:pointerdown={startDragRemoveFirstOnes} disabled={item.disabled}>{item.crossedOut ? "X" : "1"}</button>
                {/each}
            </div>
            <div/>
            {#if (operation !== "-")}
            <div/>
            <div class="numberRow tensRow secondTensElements" class:disabled={secondTensItems.disabled}>
                {#each secondTensItems.elements as item}
                    <button class="tensElement" on:pointerdown={startDragRemoveSecondTen}>
                        <div class="tenOnes">
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                            <div class="oneInTenElement">1</div>
                        </div>
                    </button>
                {/each}
            </div>
            <div/>
            <div class="numberRow onesRow secondOnesElements" class:disabled={secondOnesItems.disabled}>
                {#each secondOnesItems.elements as item}
                    <button class="onesElement removeElement" on:click={() => item = clicked(item)} on:pointerdown={startDragRemoveSecondOnes} disabled={item.disabled}>{item.crossedOut ? "X" : "1"}</button>
                {/each}
            </div>
            <div/>
            {/if}
            <div/>
            <div class="count"><h3><span class="warn">{(uncheckedTensItemsCount/10<1) ? "" : Math.floor(uncheckedTensItemsCount/10)}</span><span>{(uncheckedTensItemsCount%10)}</span></h3></div>
            <div/>
            <div class="count"><h3><span class="warn">{(uncheckedOnesItemsCount/10<1) ? "" : Math.floor(uncheckedOnesItemsCount/10)}</span><span>{uncheckedOnesItemsCount%10}</span></h3></div>
            <div></div><div/>
            <div class="addTens" >
                <button bind:this={tensAddElement} class="tensElement addElement" on:click={clicked} on:pointerdown={startDragAddTen} >
                    <div class="tenOnes">
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                        <div class="oneInTenElement">1</div>
                    </div>
                </button>
            </div>
            <div/>
            <div class="addOnes">
                <button id="addOnes1" bind:this={onesAddElement} class="onesElement addElement" on:click={clicked} on:pointerdown={startDragAddOne}>1</button>
            </div>
            <div/>
            <div/>

        </div>
    </div>
</div>
<script lang="ts">
import {  } from "svelte/internal";

    export let route;

    let firstOnesItems = {
        disabled: false,
        elements: []
    };
    let secondOnesItems = {
        disabled: false,
        elements: []
    };
    let firstTensItems = {
        disabled: false,
        elements: []
    };
    let secondTensItems = {
        disabled: false,
        elements: []
    };

    let onesAddElement;
    let tensAddElement;

    let draggedElement;

    let mouseClicked = false;

    function log(string) {
        console.log(string + " happened");
    }

    function startDragAddOne(event) {
        startDrag(event, {
            element: onesAddElement.cloneNode(true),
            allowDrop: (targetElement) => {
                return containsClassName(targetElement, "firstOnesElements") || containsClassName(targetElement, "secondOnesElements");
            },
            action : (targetElement) => {
                if(containsClassName(targetElement, "firstOnesElements")) {
                    addFirstOnesElement();
                }
                if(containsClassName(targetElement, "secondOnesElements")) {
                    addSecondOnesElement();
                }
            }
        });
    }

    function startDragRemoveFirstOnes(event) {
        startDrag(event, {
            element: onesAddElement.cloneNode(true),
            action : (targetElement) => {
                if(!containsClassName(targetElement, "OnesElements")) {
                    removeFirstOnesElement();
                }
            }
        });
    }

    function startDragRemoveSecondOnes(event) {
        startDrag(event, {
            element: onesAddElement.cloneNode(true),
            action : (targetElement) => {
                if(!containsClassName(targetElement, "OnesElements")) {
                    removeSecondOnesElement();
                }
            }
        });
    }

    function startDragAddTen(event) {
        startDrag(event, {
            element: tensAddElement.cloneNode(true),
            action : (targetElement) => {
                if(containsClassName(targetElement, "firstTensElements")) {
                    addFirstTensElement();
                }
                if(containsClassName(targetElement, "secondTensElements")) {
                    addSecondTensElement();
                }
            }
        });
    }

    function startDragRemoveFirstTen(event) {
        event.target.disabled = true;
        startDrag(event, {
            element: tensAddElement.cloneNode(true),
            action : (targetElement) => {
                event.target.disabled = false;
                if(containsClassName(targetElement, "firstOnesElements")) {
                    removeFirstTensElement();
                    addFirstTenOnesElements();
                } else if(!containsClassName(targetElement, "TensElements")) {
                    removeFirstTensElement();
                }
            }
        });
    }

    function startDragRemoveSecondTen(event) {
        event.target.disabled = true;
        startDrag(event, {
            element: tensAddElement.cloneNode(true),
            action : (targetElement) => {
                event.target.disabled = false;
                if(containsClassName(targetElement, "secondOnesElements")) {
                    removeSecondTensElement();
                    addSecondTenOnesElements();
                } else if(!containsClassName(targetElement, "TensElements")) {
                    removeSecondTensElement();
                }
            }
        });
    }
    
    function startDragMoveTenOnesToOneTen(event) {
        const onesToRemove = [];
        const secondOnesToRemove = [];
        for(let i=secondOnesItems.elements.length-1; i>=0 && onesToRemove.length<10; i--) {
            let oneToRemove = secondOnesItems.elements[i];
            oneToRemove.disabled = true;
            secondOnesToRemove.push(oneToRemove);
            onesToRemove.push(oneToRemove);
        }
        const firstOnesToRemove = []
        for(let i=firstOnesItems.elements.length-1; i>=0 && onesToRemove.length<10; i--) {
            let oneToRemove = firstOnesItems.elements[i];
            oneToRemove.disabled = true;
            firstOnesToRemove.push(oneToRemove);
            onesToRemove.push(oneToRemove);
        }

        startDrag(event, {
            element: tensAddElement.cloneNode(true),
            action : (targetElement) => {
                for(let index in onesToRemove) {
                    onesToRemove[index].disabled = false;
                }
                if(containsClassName(targetElement, "firstTensElements")) {
                    addFirstTensElement();
                    for(let index in secondOnesToRemove) {
                        removeSecondOnesElement();
                    }
                    for(let index in firstOnesToRemove) {
                        removeFirstOnesElement();
                    }
                }
                if(containsClassName(targetElement, "secondTensElements")) {
                    addSecondTensElement();
                    for(let index in secondOnesToRemove) {
                        removeSecondOnesElement();
                    }
                    for(let index in firstOnesToRemove) {
                        removeFirstOnesElement();
                    }
                }
            }
        })
    }


    function startDrag(event, dragElement) {
        mouseClicked = true;
        if(draggedElement) {
            console.log("Removing element")
            draggedElement = null;
        }
        draggedElement = dragElement;
    }

    function drag(event) {
        if(mouseClicked) {  
            if(draggedElement && draggedElement.element) {
                if(!draggedElement.element.parentElement) {
                    draggedElement.element.style.position = 'absolute';
                    draggedElement.element.style.zIndex = 1000;
                }
                if(!draggedElement.elementAdded) {
                    document.body.appendChild(draggedElement.element);
                    draggedElement.elementAdded = true;
                }
                draggedElement.element.style.left = (event.pageX - draggedElement.element.offsetWidth/2) +'px';
                draggedElement.element.style.top = (event.pageY - draggedElement.element.offsetHeight/2)+'px';

                if(draggedElement.allowDrop) {
                    try{
                        if(draggedElement.elementAdded) {
                            document.body.removeChild(draggedElement.element);
                        }
                    }catch(ignore) {
                        console.log(ignore);
                    }
                    const target = document.elementFromPoint(event.pageX , event.pageY);
                    document.body.appendChild(draggedElement.element);
                    draggedElement.element.classList.remove("noDrop");
                    if(!draggedElement.allowDrop(target)) {
                        console.log("no drop allowed");
                        draggedElement.element.classList.add("noDrop");
                        console.log(draggedElement.element.className)
                    } 
                }
            }
        }
    }
    function addFirstOnesElement() {
        firstOnesItems.elements = [...firstOnesItems.elements, {id: firstOnesItems.elements.length + 1, title: "1", crossedOut: false}];
        firstOnesItems = firstOnesItems;
    }
    function addSecondOnesElement() {
        secondOnesItems.elements = [...secondOnesItems.elements, {id: secondOnesItems.elements.length + 1, title: "1", crossedOut: false}];
        secondOnesItems = secondOnesItems;
    }
    function addFirstTensElement() {
        firstTensItems.elements = [...firstTensItems.elements, {id: firstTensItems.elements.length + 1, title: "1", crossedOut: false}];
        firstTensItems = firstTensItems;
    }
    function addSecondTensElement() {
        secondTensItems.elements = [...secondTensItems.elements, {id: secondTensItems.elements.length + 1, title: "1", crossedOut: false}];
        secondTensItems = secondTensItems;
    }

    function addFirstTenOnesElements() {
        firstOnesItems.elements = [...firstOnesItems.elements, 
            {id: firstOnesItems.elements.length + 1, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 2, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 3, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 4, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 5, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 6, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 7, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 8, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 9, title: "1", crossedOut: false},
            {id: firstOnesItems.elements.length + 10, title: "1", crossedOut: false}
        ];
        firstOnesItems = firstOnesItems;
    }

    function addSecondTenOnesElements() {
        secondOnesItems.elements = [...secondOnesItems.elements, 
            {id: secondOnesItems.elements.length + 1, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 2, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 3, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 4, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 5, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 6, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 7, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 8, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 9, title: "1", crossedOut: false},
            {id: secondOnesItems.elements.length + 10, title: "1", crossedOut: false}
        ];
        secondOnesItems = secondOnesItems;
    }

    function removeFirstOnesElement() {
        if(firstOnesItems.elements.length > 0) {
            firstOnesItems.elements.splice(firstOnesItems.elements.length - 1, 1);
            firstOnesItems = firstOnesItems;
        }
    }

    function removeSecondOnesElement() {
        if(secondOnesItems.elements.length > 0) {
            secondOnesItems.elements.splice(secondOnesItems.elements.length - 1, 1);
            secondOnesItems = secondOnesItems;
        }
    }

    function removeFirstTensElement() {
        if(firstTensItems.elements.length > 0) {
            firstTensItems.elements.splice(firstTensItems.elements.length - 1, 1);
            firstTensItems = firstTensItems;
        }
    }

    function removeSecondTensElement() {
        if(secondTensItems.elements.length > 0) {
            secondTensItems.elements.splice(secondTensItems.elements.length - 1, 1);
            secondTensItems = secondTensItems;
        }
    }

    function mouseup(event) {
        mouseClicked = false;
        if(draggedElement) {
            try{
                if(draggedElement.elementAdded) {
                    document.body.removeChild(draggedElement.element);
                }
            }catch(ignore) {
                console.log(ignore);
            }
            const target = document.elementFromPoint(event.pageX , event.pageY);

            if(draggedElement.action) {
                draggedElement.action(target);
            }

        }
        draggedElement = null;
    }
    
    function containsClassName(element, className) {
        if(element) {
            if(element.className && element.className.includes(className)){
                return true;
            } else if(element.parentElement) {
                return containsClassName(element.parentElement, className);
            }
        }
        return false;
    }

    function clicked(item) {
        if(operation === "-") {
            item.crossedOut = !item.crossedOut;
            firstOnesItems = firstOnesItems;
            secondOnesItems = secondOnesItems;
            firstTensItems = firstTensItems;
            secondTensItems = secondTensItems;
        }
        mouseClicked = false;
        return item;
    }

    document.body.addEventListener("pointerup", mouseup);
    document.body.addEventListener("pointermove", drag);

    $: uncheckedFirstOnesItemsCount = firstOnesItems.elements.filter(anItem => !anItem.crossedOut).length;
    $: uncheckedSecondOnesItemsCount = secondOnesItems.elements.filter(anItem => !anItem.crossedOut).length;

    $: uncheckedFirstTensItemsCount = firstTensItems.elements.filter(anItem => !anItem.crossedOut).length;
    $: uncheckedSecondTensItemsCount = secondTensItems.elements.filter(anItem => !anItem.crossedOut).length;

    $: uncheckedOnesItemsCount = uncheckedFirstOnesItemsCount + uncheckedSecondOnesItemsCount;
    $: uncheckedTensItemsCount = uncheckedFirstTensItemsCount + uncheckedSecondTensItemsCount;

    function parseEquation(anEquation) {
            if(anEquation) {
                const split = anEquation.split(/([+-]{1})/);
                if(split.length === 3 && !isNaN(split[0]) && !isNaN(split[2])) {
                    return {
                        number1: Number(split[0]),
                        operation: split[1],
                        number2: Number(split[2])
                    };
                }
            }
    }

    function reset(ignore) {
        firstOnesItems = {
            disabled: false,
            elements: []
        };
        secondOnesItems = {
            disabled: false,
            elements: []
        };
        firstTensItems = {
            disabled: false,
            elements: []
        };
        secondTensItems = {
            disabled: false,
            elements: []
        };
    }

    let equation = parseEquation(route?.query?.equation);

    $: number1 = equation?.number1;
    $: operation = equation?.operation;
    $: number2 = equation?.number2;

    $: reset(operation);

</script>