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




The JSON defines the left hand menu in the menu property.

```JSON
{
  "menu": []
}
```

#### CONTAINER:V1

Inside the menu is an array of containers.

```JSON
{
  "menu": [
    {
      "data": [],
      "type": "CONTAINER:V1",
      "header": "Notice",
      "isShowing": {
        "prop": "isNoticeShowing"
      }
    },
  ]
}
```

|Property|type|Required|Meaning|
|---|---|---|---|
|data|array| true | This will hold the inputs for the users|
|type|"CONTAINER:V1"| true |This is a container, this is the type for the container|
|header|string| true | These are the words on top of the container to help the user ID what the container is for |
|isShowing|Object.prop| false| This creates a switch for the user to toggle on and off the region the container is for in the component. Similar to highlighting but can also be used to turn off regions in the component. |

<br />
<br />

### Container data[]

#### TEXTFIELD:V1

|Property|type|Required|Meaning|
|---|---|---|---|
|prop|string| true | This is the name of the property attached to the props.data.user object that is injected into the react component. |
|type|"TEXTFIELD:V1"| true |This is a Textfield |
|label|string| false | The label for the text field. |
|placeholder|string| false| The placeholder example text in the textfield. |
|defaultValue|string|false| The data loaded in the textfield. |

```JSON
{
  "menu": [
    {
      "data": [{
        "prop": "textFieldProp",
        "type": "TEXTFIELD:V1",
        "label": "Example Title",
        "placeholder": "Example Placeholder",
        "defaultValue": "This is default text."
      }],
      "type": "CONTAINER:V1",
      "header": "Example",
      "isShowing": {
        "prop": "isExampleShowing"
      }
    },
  ]
}
```

What this would look like in the react component:

```JSX
import React from 'react';

function PropExample(props) {
  
  const { user, system } = props;

  return <p>{user.textFieldProp}</p>
}

export default PropExample


```

#### LINK_SELECTION:V1

#### COLOR_SELECTION:V1

#### SWITCH:V1



<!--


``` json
{
  "menu": [
    {
      "data": [
        {
          "prop": "noticeTitle",
          "type": "TEXTFIELD:V1",
          "label": "Title",
          "placeholder": "Important notice goes here."
        },
        {
          "prop": "noticeLink",
          "type": "LINK_SELECTION:V1",
          "label": "Link"
        },
        {
          "prop": "noticeColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(228, 228, 231)",
            "suggestedTextColor": "DARK"
          }
        },
        {
          "prop": "noticeColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(39, 39, 42)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Notice",
      "isShowing": {
        "prop": "isNoticeShowing"
      }
    },
    {
      "data": [
        {
          "prop": "navColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(168, 162, 158)",
            "suggestedTextColor": "DARK"
          }
        },
        {
          "prop": "navColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(77, 77, 77)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Navigation Bar",
      "isShowing": {
        "prop": "isNavShowing"
      }
    },
    {
      "data": [
        {
          "prop": "isLogoShowing",
          "type": "SWITCH:V1",
          "label": "Show Logo",
          "defaultValue": true
        },
        {
          "prop": "logo",
          "type": "MEDIA_SELECTION:V1",
          "label": "Logo",
          "fileFilter": [
            "images"
          ]
        },
        {
          "prop": "isBrandTextShowing",
          "type": "SWITCH:V1",
          "label": "Show Text",
          "defaultValue": true
        },
        {
          "prop": "brandText",
          "type": "TEXTFIELD:V1",
          "label": "Text",
          "placeholder": "Your Brand"
        },
        {
          "prop": "brandLink",
          "type": "LINK_SELECTION:V1",
          "label": "Link"
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Branding",
      "isShowing": {
        "prop": "isBrandShowing"
      }
    },
    {
      "data": [
        {
          "prop": "isFacebookShowing",
          "type": "SWITCH:V1",
          "label": "Show Facebook",
          "isShowing": "organization.hasFacebook"
        },
        {
          "prop": "isXShowing",
          "type": "SWITCH:V1",
          "label": "Show 𝕏",
          "isShowing": "organization.hasX"
        },
        {
          "prop": "isInstagramShowing",
          "type": "SWITCH:V1",
          "label": "Show Instagram",
          "isShowing": "organization.hasInstagram"
        },
        {
          "prop": "isLinkedInShowing",
          "type": "SWITCH:V1",
          "label": "Show LinkedIn",
          "isShowing": "organization.hasLinkedIn"
        },
        {
          "prop": "isYoutubeShowing",
          "type": "SWITCH:V1",
          "label": "Show FacebookYoutube",
          "isShowing": "organization.hasYoutube"
        },
        {
          "prop": "isPinterestShowing",
          "type": "SWITCH:V1",
          "label": "Show Pinterest",
          "isShowing": "organization.hasPinterest"
        },
        {
          "prop": "issocialWhatsappShowing",
          "type": "SWITCH:V1",
          "label": "Show socialWhatsapp",
          "isShowing": "organization.hassocialWhatsapp"
        },
        {
          "prop": "isRedditShowing",
          "type": "SWITCH:V1",
          "label": "Show Reddit",
          "isShowing": "organization.hasReddit"
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Social",
      "isShowing": {
        "prop": "isSocialShowing"
      }
    },
    {
      "data": [
        {
          "prop": "dayNightSelectorColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Drop Down",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(120, 113, 108)",
            "suggestedTextColor": "DARK"
          }
        },
        {
          "prop": "dayNightSelectorColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Drop Down",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(87, 83, 78)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Day/Night Selector",
      "isShowing": {
        "prop": "isDayNightSelectorShowing"
      }
    },
    {
      "data": [
        {
          "prop": "callToActionTitle",
          "type": "TEXTFIELD:V1",
          "label": "Title",
          "placeholder": "Contact"
        },
        {
          "prop": "callToActionLink",
          "type": "LINK_SELECTION:V1",
          "label": "Go To"
        },
        {
          "prop": "callToActionColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Button Color",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(228, 228, 231)",
            "suggestedTextColor": "DARK"
          }
        },
        {
          "prop": "callToActionColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Button Color",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(39, 39, 42)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Call To Action",
      "isShowing": {
        "prop": "isCallToActionShowing"
      }
    },
    {
      "data": [
        {
          "prop": "linkBoxColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(120, 113, 108)",
            "suggestedTextColor": "LIGHT"
          }
        },
        {
          "prop": "linkBoxColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(120, 113, 108)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Link Boxes",
      "isShowing": {
        "prop": "isLinkBoxShowing"
      }
    }
  ]
}
```
























{
      "data": [
        {
          "prop": "noticeTitle",
          "type": "TEXTFIELD:V1",
          "label": "Title",
          "placeholder": "Important notice goes here."
        },
        {
          "prop": "noticeLink",
          "type": "LINK_SELECTION:V1",
          "label": "Link"
        },
        {
          "prop": "noticeColorDay",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isDayMode",
          "defaultValue": {
            "color": "rgb(228, 228, 231)",
            "suggestedTextColor": "DARK"
          }
        },
        {
          "prop": "noticeColorNight",
          "type": "COLOR_SELECTION:V1",
          "label": "Background",
          "isShowing": "isNightMode",
          "defaultValue": {
            "color": "rgb(39, 39, 42)",
            "suggestedTextColor": "LIGHT"
          }
        }
      ],
      "type": "CONTAINER:V1",
      "header": "Notice",
      "isShowing": {
        "prop": "isNoticeShowing"
      }
    }, -->