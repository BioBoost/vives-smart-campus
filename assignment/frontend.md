---
description: This page describes the frontend of the application. by Gabriel Quirschfeld.
---

# Frontend

## Used technologies

It was suggested in the Software Design page of the assignment information that the frontend should be written in JavaScript. I was already familiar with node-js and with its REACT.js framework so I used these.

The biggest advantage of REACT.js is the sheer amount of useful third-party libraries and components that are free to use without any licensing issues. Having to design an interactive floor plan I found a component called react-image-mapper \([https://www.npmjs.com/package/react-image-mapper](https://www.npmjs.com/package/react-image-mapper)\). Highcharts \([https://www.highcharts.com](https://www.highcharts.com/)\) was used for displaying the historical values. Bootstrap \([https://getbootstrap.com](https://getbootstrap.com/)\) provided the necessary UI elements like forms, selectors, buttons and also the layout. Router \([https://github.com/ReactTraining/react-router](https://github.com/ReactTraining/react-router)\) was needed to set up separate router for the individual components so that they wouldn't collide in any way. Momentjs \([https://momentjs.com](https://momentjs.com/)\) was also used for time displaying formatting.

## Design

I tried to keep the overall design of the application as minimalistic and material as possible. I chose a cold color scheme with the noticeable exception being the floor plan which uses vivid color like orange to stand out from the rest of the app.

The application is designed for computers. I did not focus on the mobile design because of problems with the react-image-mapper component which did not behave correctly on small devices.

### Navigation

I chose to use the navigation bar that is available in Bootstrap. As with all of its components Bootstrap provided easy customizability. Everything but the login form is pinned to the left side. The VIVES logo and Smart Campus text are clickable and send the user back to the homepage. The other left-sided links send the user to the correct route.

The login form already had text detection implemented so it requires an email and a password to let the user send the data through. For the login button, I didn't have it detect keystrokes so hitting the enter key on the keyboard does not trigger it.

![The navbar](../.gitbook/assets/nav.png)

### Page layouts

#### Home

The homepage only contains a background image stating the name of the application. I didn't find it necessary to include anything else.

![The homepage](../.gitbook/assets/hmpg.png)

#### Building

The Building route contains the floor plan which was created by the react-image-mapper component.

```text

```

#### Devices

The Devices route contains three buttons that stretch through the upper-center part of the screen. Upon clicking on one of them the list of currently active devices/sensors/locations is displayed on the left and the form for adding a new one is on the right.

#### Calendar

This route was not abandoned because of time constraints in the hardware development part of the project.

## Code

### Building

