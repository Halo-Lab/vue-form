# @halo-lab/vue-form

The package supports simple form services such as `Formspree.io`, `Formsubmit.co`, `W3Form`. All you need is either provide URL address for the form submission, or submit callback function to the `Form` component. If chosen form service accepts the hidden input with any information, e.g. api key, you can add it as `Input` component with the name you need and the parameter `defaultValue`.

### To install the package

```sh
yarn add @halo-lab/vue-form
or
npm install @halo-lab/vue-form
```

### To use the form in the component

- import all components

```sh
import {
  Form,
  Label,
  Input,
  TextArea,
  Button
} from '@halo-lab/vue-form'
```

- import styles

```sh
<style>
@import "@halo-lab/vue-form/styles";
</style>
```

- ### `Form` is the container for all inputs. It accepts next parameters:

  - `:postUrl` (required parameter, string) - the URL address to which you need to make a `POST` request in order to submit the form. If `submitHandler` is provided, the parameter becomes optional
  - `submitHandler` (optional parameter, function) - your custom submit handler (will be responsible for submitting the form on your platform and should receive values of the form). If not provided, `:formId` is required
  - `className` (optional parameter, string) - class name for custom styling


- ### Inputs for the form:

  - #### `Input` and `TextareaComponent` accept parameters:

    - `placeholder` (required parameter, string) - the placeholder in an input field
    - `type` (required parameter, string) - the type of an input, may be `text`, `email` or `number`
    - `name` (required parameter, string) - the name of an input field
    - `label` (required parameter , string) - the label of an input field
    - `validator` (optional parameter) - the array of objects in form of `[name: <validatorKey>, message<optional>: <validatorMessage>, parameter<required for max, min, maxLength, minLength, regexp>: <validatorValue>`.
      Validator's names may be:
      - `required`,
      - `email`,
      - `number`,
      - `maxLength` (must be provided the `<validatorValue>`),
      - `minLength` (must be provided the `<validatorValue>`),
      - `max` (must be provided the `<validatorValue>`),
      - `min` (must be provided the `<validatorValue>`),
      - `regexp` (must be provided the `<validatorValue>`),
      - `func` (must be provided the `<validatorValue>`) - the validation function, which returns a truthy value if an error is detected, and a message for an error.
        For example: `[{name: "required"}, {name: "email", message: "Please, enter a valid email"}, {name: "max", message: "should be a number!", value: 6}, {name: regexp, value: /^[0-9]*$/}]`.
    - `defaultValue` (optional parameter, string) - the default value of an input
    - `fieldClassName` (optional parameter, string) - the class name for custom input container styling
    - `labelClassName` (optional parameter, string) - the class name for custom label styling
    - `inputClassName` (optional parameter, string) - the class name for custom input styling
    - `errorClassName` (optional parameter, string) - the class name for custom error state styling
    - `isDisabled` (optional parameter, boolean) - the flag to make an input field disabled

  - #### `Select` accepts parameters:

    - `name` (required parameter, string) - the name of an input field
    - `label` (required parameter , string) - the label of an input field
    - `options` (required parameter) - the array of objects in form of `{label: <display value>, value: <option value>}`
    - `validator` (optional parameter) - the array of objects in the form of `{name: <validatorKey>, message<optional>: <validatorMessage>, parameter<required for max, min, maxLength, minLength, regexp>: <validatorValue>}`.
      The validator's name may be:
      - `required`,
        For example: `[{name: "required", message: "Please, select a city"}`.
    - `search` (optional parameter, boolean) - the flag if using searchable select
    - `defaultValue` (optional parameter, string) - the default value of the input
    - `fieldClassName` (optional parameter, string) - the class name for custom input container styling
    - `labelClassName` (optional parameter, string) - the class name for custom label styling
    - `inputClassName` (optional parameter, string) - the class name for custom input styling
    - `errorClassName` (optional parameter, string) - the class name for custom error state styling
    - `isDisabled` (optional parameter, boolean) - the flag to make an input field disabled

  - #### `RadioGroup` - accepts parameters:

    - `name` (required parameter, string) - the name of an input field
    - `label` (required parameter , string) - the label of an input field
    - `fields` (required parameter) - the array of objects in form of `{value: <input value>, label: <input label>, <checked>: <boolean flag if the input should be checked default>}`
    - `fieldClassName` (optional parameter, string) - the class name for custom input container styling
    - `labelClassName` (optional parameter, string) - the class name for custom label styling
    - `inputClassName` (optional parameter, string) - the class name for custom input styling
    - `inputLabelClassName` (optional parameter, string) - the class name for custom label styling
    - `isDisabled` (optional parameter, boolean) - the flag to make an input field disabled

  - #### `CheckBoxGroup` - accepts parameters:
    - `name` (required parameter, string) - the name of an input field
    - `label` (required parameter , string) - the label of an input field
    - `fields` (required parameter) - the array of objects in form of `{value: <input value>, label: <input label>}`
    - `fieldClassName` (optional parameter, string) - the class name for custom input container styling
    - `labelClassName` (optional parameter, string) - the class name for custom label styling
    - `inputClassName` (optional parameter, string) - the class name for custom input styling
    - `inputLabelClassName` (optional parameter, string) - the class name for custom label styling
    - `isDisabled` (optional parameter, boolean) - the flag to make an input field disabled
  
  - #### `Button` accepts parameters:
    - `label` (required parameter, string) - the text for the button's label
    - `type` (optional parameter, string) - the type of the button
    - `className` (optional parameter, string) - the class name for custom button styling


### Example

```sh
    <Form  :postUrl="postUrl">
      <Input name="access_key" type="hidden" :defaultValue="key" />
      <Input 
        fieldClassName="myField" 
        inputClassName="inputMy" 
        errorClassName="error" 
        labelClassName="myLabel" 
        type="text"
        placeholder="Your Name" 
        name="name" 
        :validator="[
          { name: 'required' },
          { name: 'letters' }
        ]" 
        label="Your Name" 
      />
      <Input 
        placeholder="Email Address" 
        type="email" name="email" 
        :validator="[{ name: 'required' }, { name: 'email' }]"
        label="Email Address" 
      />
      <TextArea 
        label="Message" 
        placeholder="Message" 
        name="message" 
        :validator="[{ name: 'required' }]" 
      />
      <Select 
        label="Your City" 
        name="city" 
        search
        :validator="[{ name: 'required' }]"
        :options="[
          { label: 'New York', value: 'New York' }, 
          { label: 'Paris', value: 'Paris' }, 
          { label: 'Kyiv', value: 'Kyiv' }
          ]" 
      />
      <RadioGroup 
        label="Your Gender" 
        name="gender"
        :fields="[
          {value: 'male', label: 'Male'}, 
          {value: 'female', label: 'Female', checked: true}
          ]" 
        />
      <CheckBoxGroup 
        label="Your Favorite food" 
        name="food"
        :fields="[
          { value: 'chocolate', label: 'Chocolate' }, 
          { value: 'ice-cream', label: 'Ice-cream' }, 
          { value: 'coffee', label: 'Coffee' }
        ]" 
      />
      <Button label="Send form" type="submit" className="button-filledMy" />
    </Form>
```

## Word from the author

Have fun ✌️

<a href="https://www.halo-lab.com/?utm_source=github">
  <img
    src="https://dgestran.sirv.com/Images/supported-by-halolab.png"
    alt="Supported by Halo lab"
    height="60"
  >
</a>
