# MutationObserver

## 1 MutationObserver Using Summary

When using MutationObserver, you should pay attentation to the following points:

* Limit the scope and type of observation to improve performance;
* Make sure to call `disconnect()` to stop observation when not needed to avoid memory leaks;
* Avoid causing infinite loops directly in callbacks;
* By cautions when using subtree and other parameters to balance functionality and performance overhead;
* Through reasonable configuration and optimization, you can efficiently use MutationObserver to monitor and operate DOM changes.

## 2 Use MutationObserver

Through reasonable configuration and optimization, `MutationObserver` can be used efficiently to monitor and operate DOM changes.

MutationObserver monitors DOM changes. If it is not configured properly, the monitoring range is too large, or the callback function is triggered frequently, it may cause performance degradtion. To avoid performance issues, the following aspects schould be considered.

## Limit the scope of observation

Limit the scope of observation, try to avoid observing the entire document, and only observe the specific nodes you care about.

```js
observer.observe(document.getElementById('specificElement'), {childList: true, subtree: true});
```

## Reasonably set configuration parameters

Reasonably set configuration parameters: By setting options such as `childList`, `attributes`, `characterData`, etc., try to reduce unnecessary monitoring.

```js
const config = {
    childList: true, // motitor changes in child nodes (addition, deletion)
    subtree: false, // whether to expand to the entire subtree (set to true to monitor all descendants)
    attributes: false,  // whether to monitor property changes
    characterData: false // whether to monitor changes in text content
}
```

## Merge mutiple changes

Merge mutiple changes: MutationObserver passes all the changes that occur to the callback function in a batch. Using this, you can batch process changes to avoid triggering too many operations for a single change.

```js
const observer = new MutationObserver((mutationsList) => {
    mutationsList.forEach((mutation) => {
        if (mutation.type === 'childList') {
            // batch process changes
        }
    })
})
```

## Disconnect method

Disconnect() method, MutationObserver starts observing DOM changes, it will continue to monitor unless manually stopped. To avoid memory leaks or unnecessary performance consumption, when observation is no longer needed, the `disconnect()` method should be called to stop observation.

```js
observer.disconnect(); // stop monitor
```

## Avoid infinite loops

Avoid infinite loops, when the code modifies the DOM in the callback monitored by MutationObserver, it may cause an infinite loop observation and callback. If you need to modify the DOM in the callback, make sure that it does not cause repeated observation.

```js
const observer = new MutationObserver((mutationsList) => {
    observer.disconnect(); // temporarily stop monitoring to prevent callbacks from causing an inifinite loop
    mutationsList.forEach((mutation) => {
        // modify the DOM or perform related operations
    });
    observer.observe(targetNode, config); // restart monitoring after modification
})
```

## Set subtree attributes

when `subtree: true`, `MutationObserver` will monitor the entire subtree for all changes. This may increase performance overhead, so it is recommended to enable it only when necessary. If you only care about changes to direct child nodes, you can set `subtree: false`.

## Set attributes or characterData

If you only care about changes to the attributes or text content of an element, you can monitor those changes separately by setting attributes or characterData. To avoid performance waste, make sure to enable these monitors only when you really need them.

```js
const config = {
    attributes: true, // monitor changes to attrabutes
    attributeFilter: ['class', 'id'], // only monitor changes to specific attributes
    characterData: true, // monitor changes to text content
}
```

## Proper error handling

Proper error handling, when performing DOM operations in callback functions, sometimes errors may occur due to unexpected DOM structures or other error conditions. Therefore , mack sure to add error handling mechanisms to the callback to improve the robustness of the code.

```js
const observer = new MutationObserver((mutationsList) => {
    try {
        mutationsList.forEach((mutation) => {
            // perform safe DOM operations
        })
    } catch (error) {
        console.error('MutationObserver error:', error);
    }
})
```

