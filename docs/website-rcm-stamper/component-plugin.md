# Component Plugins

This documentation is about creating a plugin in the WebsiteRCM application. This application is known as a React Component Manager, similar to a CMS (Content Management System) for React components.

*Tip:* Think React.js without frameworks, so no JavaScript framework or CSS framework.

*Tip:* You should modularize all CSS in each component you create.

<br /><br /><br />

## Component Creation Instructions

A component is built with two things working together:
1. A React component
2. A JSON file that creates the left-hand menu and the `props.data.user` object.

-------

Every React component you create will be injected with the following props:

```jsx
import React from 'react';

function PropExample(props) {
  
  const { user, system } = props.data;
  const {
    // env
    isDisplayMode,
    isFunctionalMode,
    isDevMode,
    isProdMode,
    // colors
    isDayMode,
    isNightMode,
  } = system.state

  const {
    column,
  } = system.setting

  return <p>Prop Example</p>
}

export default PropExample

```

<br />
<br />

### props.data.system.state
| property | type | meaning|
|---|---|---|
|isDisplayMode| boolean | If true, it is the pretty version that is selected by the user. the developer controls the content. |
|isFunctionalMode| boolean |This means the user should control the content. If this is true, it means that one of the following properties is true: isDevMode or isProdMode. |
|isDevMode| boolean | This means it is in the portal being edited. |
|isProdMode| boolean | It has been published and is on the front website.|
|isDayMode| boolean | It means brighter colors are being selected|
|isNightMode | boolean | It means darker colors are being selected|

<br />

*Tip:* If display mode is on, functionality mode is off. And if functionality mode is on, display mode is off. This could have been an enum, but this would be an extra thing to remember when simplicity is the goal. So instead of being an enum, both of these properties can not be false or true at the same time, one is true and the other is false.

*Tip:* If functionality mode is on, that means dev or production is on. Dev and prod mode will not be on at the same time.

*Tip:* If display mode is on, than functionality, dev, and production is off. 

*Tip:* This data is always be available in every component you create.

<br />
<br />
### `props.data.system.state`
| Property | Type | Meaning |
|---|---|---|
| isDisplayMode | boolean | If true, it is the pretty version selected by the user. The developer controls the content. |
| isFunctionalMode | boolean | This means the user controls the content. If this is true, one of the following properties is also true: isDevMode or isProdMode. |
| isDevMode | boolean | This means it is in the portal being edited. |
| isProdMode | boolean | It has been published and is on the front website. |
| isDayMode | boolean | It means brighter colors are being selected. |
| isNightMode | boolean | It means darker colors are being selected. |

<br />

*Tip:* If display mode is on, functionality mode is off, and vice versa. This could have been an enum, but simplicity is the goal. Both properties cannot be true or false at the same time; one is true, and the other is false.

*Tip:* If functionality mode is on, either dev or production mode is on. Dev and prod mode will not be on at the same time.

*Tip:* If display mode is on, functionality, dev, and production modes are off.

*Tip:* This data will always be available in every component you create.

<br /><br />

### `props.data.system.setting`
| Property | Type | Meaning |
|---|---|---|
| column | string | It is the max width of the component for large screens. It is best to center the div with `margin: 0 auto` to ensure your website looks great on bigger screens. |

*Tip:* This data will always be available in every component you create.

<br /><br />

### `props.data.user`

This is the data from the left-hand menu being injected into the props. It is called `props.data.user` because the data comes from the user in the editor. Each component has a different version of this, but components can use the same data.

*Tip:* The properties are not guaranteed to be there.

*Tip:* The JSON file determines the structure of this object. Once you understand the pattern, it will be very simple to use.

*Tip:* The designer uses TypeScript to match the type with the JSON to reduce errors.

*Tip:* If you build a component that uses the same JSON property names, you can swap out components.

*Tip:* Deleting a component doesn't mean you lose the user data (`props.data.user`). This allows a new upgraded component to be selected and the data transferred. Even if you delete the component first, the data will persist. You can override the property names, so try to pick unique property names per component unless you are trying to switch out components.

*Tip:* One user answer per left menu JSON file per React component.

<br />

WebsiteRCM consists of three things working together:

| Data Point | Author |
| --- | --- |
| The React component | The programmer |
| The left menu JSON file | The programmer |
| The answers from the left menu JSON file (user data) | The business analyst |

<br /><br />

## The JSON file

The JSON file is built by listing the data selection options you want to see on the left-hand menu. These options are selected in a real-time environment and try to persist as long as possible, but they can be overwritten.
