# Choices.js [![Build Status](https://travis-ci.org/jshjohnson/Choices.svg?branch=master)](https://travis-ci.org/jshjohnson/Choices) 
A vanilla, lightweight (~15kb gzipped 🎉), configurable select box/text input plugin. Similar to Select2 and Selectize but without the jQuery dependency.

[Demo](https://joshuajohnson.co.uk/Choices/)

## Setup

```html
<!-- Include base CSS (optional) -->
<link rel="stylesheet" href="assets/styles/css/base.min.css">
<!-- Include Choices CSS -->
<link rel="stylesheet" href="assets/styles/css/choices.min.css">
<!-- Include Choices JavaScript -->
<script src="/assets/scripts/dist/choices.min.js"></script>
<script>
    // Pass multiple elements:
    const choices = new Choices(elements);
    
    // Pass single element:
    const choices = new Choices(element);
    
    // Pass reference
    const choices = new Choices('[data-choice']);
    const choices = new Choices('.js-choice');

    // Pass jQuery element
    const choices = new Choices($('.js-choice')[0]);
    
    // Passing options (with default options)
    const choices = new Choices(elements, {
        items: [],
        choices: [],
        maxItemCount: -1,
        addItems: true,
        removeItems: true,
        removeItemButton: false,
        editItems: false,
        duplicateItems: true,
        delimiter: ',',
        paste: true,
        search: true,
        flip: true,
        regexFilter: null,
        sortFilter: sortByAlpha,
        sortFields: ['label', 'value'],
        placeholder: true,
        placeholderValue: null,
        prependValue: null,
        appendValue: null,
        loadingText: 'Loading...',
        noResultsText: 'No results round',
        noChoicesText: 'No choices to choose from',
        classNames: {
            containerOuter: 'choices',
            containerInner: 'choices__inner',
            input: 'choices__input',
            inputCloned: 'choices__input--cloned',
            list: 'choices__list',
            listItems: 'choices__list--multiple',
            listSingle: 'choices__list--single',
            listDropdown: 'choices__list--dropdown',
            item: 'choices__item',
            itemSelectable: 'choices__item--selectable',
            itemDisabled: 'choices__item--disabled',
            itemChoice: 'choices__item--choice',
            group: 'choices__group',
            groupHeading : 'choices__heading',
            button: 'choices__button',
            activeState: 'is-active',
            focusState: 'is-focused',
            openState: 'is-open',
            disabledState: 'is-disabled',
            highlightedState: 'is-highlighted',
            hiddenState: 'is-hidden',
            flippedState: 'is-flipped',
            loadingState: 'is-loading',
        },
        callbackOnInit: () => {},
        callbackOnAddItem: (id, value, passedInput) => {},
        callbackOnRemoveItem: (id, value, passedInput) => {},
        callbackOnHighlightItem: (id, value, passedInput) => {},
        callbackOnUnhighlightItem: (id, value, passedInput) => {},
        callbackOnChange: (value, passedInput) => {},
    });
</script>
```

## Installation

`npm install choices.js --save`

## Terminology
| Word   | Definition |
| ------ | ---------- |
| Choice | A choice is a value a user can select. A choice would be equivelant to the `<option></option>` element within a select input.  |
| Group  | A group is a collection of choices. A group should be seen as equivalent to a `<optgroup></optgroup>` element within a select input.|
| Item   | An item is an inputted value (text input) or a selected choice (select element). In the context of a select element, an item is equivelent to a selected option element: `<option value="Hello" selected></option>` whereas in the context of a text input an item is equivelant to `<input type="text" value="Hello">`|


## Configuration options
### items
<strong>Type:</strong> `Array`  <strong>Default:</strong>  `[]`

<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> Add pre-selected items (see terminology) to text input. 

Pass an array of strings: 

`['value 1', 'value 2', 'value 3']`

Pass an array of objects:

```
[{ 
	value: 'Value 1',
	label: 'Label 1', 
	id: 1 
},
{ 
	value: 'Value 2',
	label: 'Label 2', 
	id: 2
}]
```

### choices
<strong>Type:</strong> `Array`  <strong>Default:</strong>  `[]`

<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Add choices (see terminology) to select input. 

Pass an array of objects:

```
[{ 
	value: 'Option 1',
	label: 'Option 1', 
	selected: true,
	disabled: false,
},
{ 
	value: 'Option 2',
	label: 'Option 2', 
	selected: false,
	disabled: true,
}]
```

### maxItemCount
<strong>Type:</strong> `Number` <strong>Default:</strong> `-1`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> The amount of items a user can input/select ("-1" indicates no limit).

### addItems
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> Whether a user can add items to the passed input's value.

### removeItems
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Whether a user can remove items.

### removeButton
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `false`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Whether a button should show that, when clicked, will remove an item.

### editItems
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `false`

<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> Whether a user can edit items. An items value can be edited by pressing the backspace.

### duplicateItems
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Whether a user can input/choose a duplicate item.

### delimiter
<strong>Type:</strong> `String` <strong>Default:</strong> `,`

<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> What divides each value. By default the delimited value would be `"Value 1, Value 2, Value 3"`.

### paste
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Whether a user can paste into the input.

### search
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `select-one`

<strong>Usage:</strong> Whether a user should be allowed to search avaiable choices. Note that multiple select boxes will always show search inputs.

### flip
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Whether the dropdown should appear above the input if there is not enough space within the window. 

### regexFilter
<strong>Type:</strong> `Regex` <strong>Default:</strong> `null`

<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> A filter that will need to pass for a user to successfully add an item.

### sortFilter
<strong>Type:</strong> `Function` <strong>Default:</strong> sortByAlpha

<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> The function that will sort choices before they are displayed (unless a user is searching). By default choices are sorted by alphabetical order.

<strong>Example:</strong>

```js
// Sorting via length of label from largest to smallest
const example = new Choices(element, {
    sortFilter: function(a, b) {
        return b.label.length - a.label.length;
    },
};
```

### sortFields
<strong>Type:</strong> `Array/String` <strong>Default:</strong> `['label', 'value']`

<strong>Input types affected:</strong>`select-one`, `select-multiple`

<strong>Usage:</strong> Specify which fields should be used for sorting. 

### placeholder
<strong>Type:</strong> `Boolean` <strong>Default:</strong> `true`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Whether the input should show a placeholder. Used in conjunction with `placeholderValue`. If `placeholder` is set to true and no value is passed to `placeholderValue`, the passed input's placeholder attribute will be used as the  placeholder value.

### placeholderValue
<strong>Type:</strong> `String` <strong>Default:</strong> `null`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> The value of the inputs placeholder.

### prependValue
<strong>Type:</strong> `String` <strong>Default:</strong> `null`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Prepend a value to each item added/selected.

### appendValue
<strong>Type:</strong> `String` <strong>Default:</strong> `null`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Append a value to each item added/selected.

### loadingText
<strong>Type:</strong> `String` <strong>Default:</strong> `Loading...`

<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> The text that is shown whilst choices are being populated via AJAX.

### noResultsText
<strong>Type:</strong> `String` <strong>Default:</strong> `No results round`

<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> The text that is shown when a user's search has returned no results.

### noChoicesText
<strong>Type:</strong> `String` <strong>Default:</strong> `No choices to choose from`

<strong>Input types affected:</strong> `select-multiple`

<strong>Usage:</strong> The text that is shown when a user has selected all possible choices.

### classNames
<strong>Type:</strong> `Object` <strong>Default:</strong> 

```
classNames: {
    containerOuter: 'choices',
    containerInner: 'choices__inner',
    input: 'choices__input',
    inputCloned: 'choices__input--cloned',
    list: 'choices__list',
    listItems: 'choices__list--multiple',
    listSingle: 'choices__list--single',
    listDropdown: 'choices__list--dropdown',
    item: 'choices__item',
    itemSelectable: 'choices__item--selectable',
    itemDisabled: 'choices__item--disabled',
    itemOption: 'choices__item--choice',
    group: 'choices__group',
    groupHeading : 'choices__heading',
    button: 'choices__button',
    activeState: 'is-active',
    focusState: 'is-focused',
    openState: 'is-open',
    disabledState: 'is-disabled',
    highlightedState: 'is-highlighted',
    hiddenState: 'is-hidden',
    flippedState: 'is-flipped',
    selectedState: 'is-highlighted',
}
```

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Classes added to HTML generated by Choices. By default classnames follow the [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) notation.

### callbackOnInit
<strong>Type:</strong> `Function` <strong>Default:</strong> `() => {}`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Function to run once Choices initialises.

### callbackOnAddItem
<strong>Type:</strong> `Function` <strong>Default:</strong> `(id, value, passedInput) => {}`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Function to run each time an item is added (programmatically or by the user).

### callbackOnRemoveItem
<strong>Type:</strong> `Function` <strong>Default:</strong> `(id, value, passedInput) => {}`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Function to run each time an item is removed (programmatically or by the user).

### callbackOnHighlightItem
<strong>Type:</strong> `Function` <strong>Default:</strong> `(id, value, passedInput) => {}`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Function to run each time an item is highlighted.

### callbackOnUnhighlightItem
<strong>Type:</strong> `Function` <strong>Default:</strong> `(id, value, passedInput) => {}`

<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Function to run each time an item is unhighlighted.

### callbackOnChange
<strong>Type:</strong> `Function` <strong>Default:</strong> `(value, passedInput) => {}`

<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Function to run each time an item is added/removed by a user.


## Methods
Methods can be called either directly or by chaining:

```js
// Calling a method by chaining
const choices = new Choices(element, {
    addItems: false,
    removeItems: false,
}).setValue(['Set value 1', 'Set value 2']).disable();

// Calling a method directly
const choices = new Choices(element, {
    addItems: false,
    removeItems: false,
});

choices.setValue(['Set value 1', 'Set value 2'])
choices.disable();
```

### destroy();
<strong>Input types affected:</strong> `text`, `select-multiple`, `select-one`

<strong>Usage:</strong> Kills the instance of Choices, removes all event listeners and returns passed input to its initial state.

### init();
<strong>Input types affected:</strong> `text`, `select-multiple`, `select-one`

<strong>Usage:</strong> Creates a new instance of Choices, adds event listeners, creates templates and renders a Choices element to the DOM.

<strong>Note:</strong> This is called implicitly when a new instance of Choices is created. This would be used after a Choices instance had already been destroyed (using `destroy()`). 

### highlightAll();
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Highlight each chosen item (selected items can be removed).


### unhighlightAll();
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Un-highlight each chosen item.


### removeItemsByValue(value);
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Remove each item by a given value.


### removeActiveItems(excludedId);
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Remove each selectable item.


### removeHighlightedItems();
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Remove each item the user has selected.


### showDropdown();
<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Show option list dropdown (only affects select inputs).


### hideDropdown();
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Hide option list dropdown (only affects select inputs).


### toggleDropdown();
<strong>Input types affected:</strong> `text`, `select-multiple`

<strong>Usage:</strong> Toggle dropdown between showing/hidden.

### setChoices(choices, value, label);
<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Set choices of select input via an array of objects, a value name and a label name. This behaves the same as passing items via the `choices` option but can be called after initialising Choices. This can also be used to add groups of choices (see example 2);

<strong>Example 1:</strong>

```js
const example = new Choices(element);

example.setChoices([
    {value: 'One', label: 'Label One', disabled: true},
    {value: 'Two', label: 'Label Two' selected: true},
    {value: 'Three', label: 'Label Three'},
], 'value', 'label');
```

<strong>Example 2:</strong>

```js
const example = new Choices(element);

example.setChoices([{
    label: 'Group one',
    id: 1,
    disabled: false,
    choices: [
        {value: 'Child One', label: 'Child One', selected: true},
        {value: 'Child Two', label: 'Child Two',  disabled: true},
        {value: 'Child Three', label: 'Child Three'},
    ]
}, 
{
    label: 'Group two',
    id: 2,
    disabled: false,
    choices: [
        {value: 'Child Four', label: 'Child Four', disabled: true},
        {value: 'Child Five', label: 'Child Five'},
        {value: 'Child Six', label: 'Child Six'},
    ]
}], 'value', 'label');
```

### getValue(valueOnly)
<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Get value(s) of input (i.e. inputted items (text) or selected choices (select)). Optionally pass an argument of `true` to only return values rather than value objects.

<strong>Example:</strong>

```js
const example = new Choices(element);
const values = example.getValue(true); // returns ['value 1', 'value 2'];
const valueArray = example.getValue(); // returns [{ active: true, choiceId: 1, highlighted: false, id: 1, label: 'Label 1', value: 'Value 1'},  { active: true, choiceId: 2, highlighted: false, id: 2, label: 'Label 2', value: 'Value 2'}];
```

### setValue(args);
<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> Set value of input based on an array of objects or strings. This behaves exactly the same as passing items via the `items` option but can be called after initialising Choices.

<strong>Example:</strong>

```js
const example = new Choices(element);

// via an array of objects
example.setValue([
    {value: 'One', label: 'Label One'},
    {value: 'Two', label: 'Label Two'},
    {value: 'Three', label: 'Label Three'},
]);

// or via an array of strings
example.setValue(['Four','Five','Six']);
```

### setValueByChoice(value);
<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Set value of input based on existing Choice.

<strong>Example:</strong>

```js
const example = new Choices(element, {
    choices: [
        {value: 'One', label: 'Label One'},
        {value: 'Two', label: 'Label Two', disabled: true},
        {value: 'Three', label: 'Label Three'},
    ],
});

example.setValueByChoice('Two'); // Choice with value of 'Two' has now been selected.
```

### clearStore();
<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Removes all items, choices and groups. Use with caution.


### clearInput();
<strong>Input types affected:</strong> `text`

<strong>Usage:</strong> Clear input of any user inputted text.


### disable();
<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Disables input from accepting new value/sselecting further choices.

### enable();
<strong>Input types affected:</strong> `text`, `select-one`, `select-multiple`

<strong>Usage:</strong> Enables input to accept new values/select further choices.


### ajax(fn);
<strong>Input types affected:</strong> `select-one`, `select-multiple`

<strong>Usage:</strong> Populate options via a callback.

<strong>Example:</strong>

```js
var example = new Choices(element);

example.ajax(function(callback) {
    fetch(url)
        .then(function(response) {
            response.json().then(function(data) {
                callback(data, 'value', 'label');
            });
        })
        .catch(function(error) {
            console.log(error);
        });
});
```


## Browser compatibility
ES5 browsers and above (http://caniuse.com/#feat=es5). 

## Development
To setup a local environment: clone this repo, navigate into it's directory in a terminal window and run the following command:

```npm install```

### NPM tasks
| Task                | Usage                                                        |
| ------------------- | ------------------------------------------------------------ |
| `npm start`         | Fire up local server for development                         |
| `npm run js:build`  | Compile Choices to an uglified JavaScript file               |
| `npm run css:watch` | Watch SCSS files for changes. On a change, run build process |
| `npm run css:build` | Compile, minify and prefix SCSS files to CSS                 |

## Contributions
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using npm scripts...bla bla bla

## License
MIT License 

## Misc
Thanks to [@mikefrancis](https://github.com/mikefrancis/) for [sending me on a hunt](https://twitter.com/_mikefrancis/status/701797835826667520) for a non-jQuery solution for select boxes that eventually led to this being built!
