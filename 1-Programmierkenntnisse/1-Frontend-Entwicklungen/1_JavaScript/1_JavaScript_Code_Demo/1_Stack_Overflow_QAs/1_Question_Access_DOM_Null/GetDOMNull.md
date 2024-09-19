# Query DOM NULL

Stack overflow QS: <a href="https://stackoverflow.com/questions/78936250/content-script-function-returning-null-value-after-accessing-dom-when-page-l" target="_blank">Content script – Function returning "Null" value after accessing DOM when page load has completed</a>

When querying DOM elements returns **Null**, be sure to check: 

1. Is the element selector incorrect?
2. Wheteher the element has not yet been loaded into the DOM?
3. Is it dynamically generated element?
4. 


## 1 Is the element selector incorrect ?

If you use the wrong selector, such as misspelling the ID or class name, or the selector does not conform to the actual DOM structure, the correct element cannot be obtained.

## 2 Whether the element has not yet been loaded into the DOM ?

If `addEventlistener` is called before the DOM element is loaded into the page, the element does not exist yet, so the get will return `null`.  

There are several ways to ensure that the element has been loaded:

* Put your script at the end of the `<body>` tag to ensure that the DOM is fully load;
* Using the `DOMcontentLoaded` event, this event is **triggered** when the initial HTML decument is fully loaded and parsed, that is, when the DOM tree is built. _At this point, there is no need to wait for other resources such as CSS and images to load;_
* Using the `load` event, triggered when the page and _all its dependent resources (such as images, style sheets, etc.) are fully loaded._  

## 3 Is it a dynamically generated element ?

If the element is **dynamically generated** via JavaScript, you need to make sure to get the element after it is generated.

we can use <a href="https://github.com/huabin91/mein-profil/blob/main/1-Programmierkenntnisse/1-Frontend-Entwicklungen/1_JavaScript/1_JavaScript_Code_Demo/1_Stack_Overflow_QAs/1_Question_Access_DOM_Null/MutationObserverUsing.md" target="_blank">MutationObserver</a>.

## 4 Is the `addEventListener` method called in the wrong scope or context?

If you use a local selector method on a specific context and there are no matching elements in that context, `null` will also be return.