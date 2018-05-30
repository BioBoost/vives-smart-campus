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

The Building route contains the floor plan which was created by the react-image-mapper component. Active rooms have the measured real-time values of the temperature, humidity and movement displayed over them. Clicking on a room opens the historical data of those measured values in a form of a graph.

![](../.gitbook/assets/building.png)

#### Devices

The Devices route contains three buttons that stretch through the upper-center part of the screen. Upon clicking on one of them the list of currently active devices/sensors/locations is displayed on the left and the form for adding a new one is on the right.

![](../.gitbook/assets/devices.png)

#### Calendar

This route was abandoned because of time constraints in the hardware development part of the project.

## Code

### Building

The image-mapper component was straight-forward to create. It's basically an .svg image that has areas mapper over it. The areas are determined by the current width of the browser window to be adjustable. I wasn't able to make the whole image adjustable like that without the need for a page refresh \(which in turn made it impossible to display the graph\), so I did not make it so. After changing the size of the browser window the user has to manually refresh the page for the component to change size.

```javascript
<ImageMapper
    src={require("../img/floor_plan.svg")} // the visual of the plan
    id="map"
    width={this.state.width * 0.7} // width adjustable based on browser window width
    map={this.state.MAP} // the areas mapped on the plan
    fillColor={"rgba(141, 128, 229, 0.3)"}
    onClick{(this.state.MAP.areas, this.click_handle)} // action on clicking an area
/>
```

The function for setting the areas that are mapped on the floor plan needed to be calculated precisely. By knowing the exact measurements of the rooms in the floor plan it was easy to set them correctly using the width parameter that updates every time the browser window is resized.

The data displayed over the individual rooms are just text elements of HTML. As with the areas on the plan they needed to be positioned manually with calculations depending on the width of the browser window. During the rendering of the site a function is called for each of the datatypes \(temperature, humidity and movement\).

```javascript
temp_style() {
    var temp = []; // declaring helper arrays and variables
    var arr = [];
    var margin = 0.072;
    
    for (var i = 0; i < 5; i++) {
        temp[i] = { position: 'absolute',
                    top: this.state.width * 0.15,
                    left: this.state.width * margin,
                    'fontSize': this.state.width * 0.007,
                    'fontWeight': 'bold'
                    };
        margin = margin + 0.079;
        if (i === 4) {
            temp[i] = { position: 'absolute',
                        top: this.state.width * 0.15,
                        left: this.state.width * margin,
                        'fontSize': this.state.width * 0.007,
                        'fontWeight': 'bold'
                        };
        }
        if (this.state.temp_data[i] !== undefined) {
            arr[i] = <span style={temp[i]}>
                        TEMP: {this.state.temp_data[i].value + "°C"}
                    </span>
        }
    }
    return arr;
}
```

