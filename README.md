

This is an autocomplete for procurement codes.

The code is built on top of the [accessible-autocomplete](https://github.com/alphagov/accessible-autocomplete) component, with the additional features of being able to search by abbreviation (eg 'DfE') or alternative names.


[View demo](https://frankieroberto.github.io/govuk-government-organisations-autocomplete/examples/)


## How to use

The autocomplete works as a progressive enhancement of a dropdown element. This ensures that the interface still works when javascript is unavailable.

The most basic form of the autocomplete will work with any regular `<select>` HTML, eg:

```html
<select id="government-organisation">
  <option value="" selected>Pick an option</option>
  <option value="D2">Cabinet Office</option>
  <option value="D1198">Department for Business, Energy &amp; Industrial Strategy</option>
  <option value="D5">Department for Digital, Culture, Media and Sport</option>
  <option value="D6">Department for Education</option>
  <option value="D7">Department for Environment, Food &amp; Rural Affairs</option>
</select>
```

To enhance this with the autocomplete, you’ll need to include the javascript function in [govuk_government_organisations_autocomplete.js](./src/govuk_government_organisations_autocomplete.js), and then initialize it with a reference to your select element:

```javascript
govukGovernmentOrganisationsAutocomplete({
  selectElement: document.getElementById('government-organisations'),
})
```

## Additional data and abbreviations

Additional data and abbreviations are not used at it is not believed at this point that these will be a feature of the Redwood autocomplete.

You can further improve the usability of the autocomplete by allowing users to select government organisations by their common abbreviation (such as DfE) or alternative/previous names (such as _Department for Communities and Local Government_ instead of _Ministry of Housing, Communities and Local Government_).

To do this, add the additional values as data attributes, as below:

```html
<select id="government-organisation">
  <option value="" selected>Pick an option</option>
  <option value="D2" data-abbreviations="CO">
    Cabinet Office
  </option>
  <option value="D1198" data-abbreviations="BEIS">
    Department for Business, Energy &amp; Industrial Strategy
  </option>
  <option value="D5" data-abbreviations="DCMS"
    data-other-names="Department for Culture, Media & Sport|Department for Digital, Culture Media & Sport">
    Department for Digital, Culture, Media and Sport
  </option>
  <option value="D6" data-abbreviations="DfE">
    Department for Education
  </option>
  <option value="D7" data-abbreviations="Defra"
    data-other-names="Department for Environment Food & Rural Affairs">
    Department for Environment, Food &amp; Rural Affairs
  </option>
</select>
```

(Note that these attribute names are plural, as they can take multiple values separated by a `|` character.)

If your list of organisations is long, you can group them using the `<optgroup>` element. This improves accessibility for non-javascript users:

```html
<select id="government-organisation">
  <optgroup label="Ministerial Departments">
    <option value="" selected>Pick an option</option>
    <option value="D2">Cabinet Office</option>
    <option value="D1198">Department for Business, Energy &amp; Industrial Strategy</option>
    <option value="D5">Department for Digital, Culture, Media and Sport</option>
    <option value="D6">Department for Education</option>
    <option value="D7">Department for Environment, Food &amp; Rural Affairs</option>
  </optgroup>
  <optgroup label="Non-ministerial departments">
    <option value="D550">Competition and Markets Authority</option>
    <option value="D101">Crown Prosecution Service</option>
    <option value="D102">Food Standards Agency</option>
    <option value="D85">Forestry Commission</option>
    <option value="D103">Government Actuary's Department</option>
  </optgroup>
</select>
```

### Styling

The javascript function works by first hiding the `<select>` dropdown, replacing it with a regular `<input>` element, and then adding a list of suggestions within a `<ul>` tag.

You can use the following class names to target styles:

* `autocomplete__wrapper` - overall wrapper element
* `autocomplete__input` - the input element
* `autocomplete__hint` - hint text (used if `autoSuggest` is set to `true`)
* `autocomplete__menu` - the suggestions element
* `autocomplete__option` - an individual suggetion

Alternatively, use the existing CSS in [`accessible-autocomplete.css`](./examples/vendor/accessible-autocomplete.css).

### Options

The [accessible-autocomplete](https://github.com/alphagov/accessible-autocomplete) code (on which this is based) supports additional options, including:

* `minLength` - default is `0` - minimum number of characters before options are shown.
* `autoselect` - default is `false`. Set to `true` to highlight the first option when the user types in something and receives results. Pressing enter will select it.
* `confirmOnBlur` - default is `true`. The autocomplete will confirm the currently selected option when the user clicks outside of the component. Set to false to disable.

See [autocomplete options](https://github.com/alphagov/accessible-autocomplete#other-options) for a full list.

## Source data

The source data contains the following fields:

* `key` - primary key.
* `current_name` - the current official name of the code
* `category` - any other data displayed in the autocomplete for the code
* `other_name` - NOT USED this includes previous names for the code as well as some spelling variants
* `abbreviations` – NOT USED any abbreviations (or previous abbreviations) for the code (eg `DfT` for the Department of Transport).
* `start_date` - NOT USED date or month or year organisation started (`null` implies unknown).
* `end_date` - NOT USED date or month or year organisation ended (`null` implies that the organisation still operates, `"unknown"` implies that the organisation has closed, but the date is unknown).
* `format` - NOT USED status of the organisation within Government, eg 'Ministerial department' or 'Executive agency'.
* `parents` - NOT USED the keys of any parent organisation (eg the Department that an Agency belongs to, or is sponsored by).
