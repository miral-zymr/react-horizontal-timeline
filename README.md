# React Horizontal Timeline Tooltip

This is a customized package of the original: https://github.com/sherubthakur/react-horizontal-timeline. We've tried to add the functionality of setting a custom node, for the dates on the timeline. We've also tried to remove the peer dependencies for this package.
## HorizontalTimeline

It will just render a timeline with the dates that you provided and it is up to you what to do when a date is selected. i.e. it will give you the index of the date that was clicked and you can do anything with it.

Property	                  |	Type   	     |	Default	                      |	Description
:--------------------------|:--------------|:-------------------------------|:--------------------------------
 values (**required**)     | array         | undefined                      | **sorted** array of dates (format:**yyyy-mm-dd**)
 indexClick (**required**) | function      | undefined                      | function that takes the index of the array as argument
 index (**required**)      | number        | undefined                      | the index of the selected date
 **tooltip**                   | element       |                                | Show the custom element on the date nodes of the timeline.
 getLabel                  | function      | date.toDateString().substring(4) |  A function to calculate the label of the event based on the date of the event
 minEventPadding           | number        | 20                             | The minimum padding between two event labels
 maxEventPadding           | number        | 120                            | The maximum padding between two event labels
 linePadding               | number        | 100                            | Padding used at the start and end of the timeline
 labelWidth                | number        | 85                             | The width of an individual label
 fillingMotion             | object        |{ stiffness: 150, damping: 25 } | Sets the animation style of how filling motion will look
 slidingMotion             | object        |{ stiffness: 150, damping: 25 } | Sets the animation style of how sliding motion will look
 styles                    | object        |{ background: '#f8f8f8', foreground: '#7b9d6f', outline: '#dfdfdf' } | object containing the styles for the timeline currently outline (the color of the boundaries of the timeline and the buttons on it's either side), foreground (the filling color, active color) and background (the background color of your page) colors of the timeline can be changed.
 isTouchEnabled            | boolean       | true                           | Enable touch events (swipe left, right)
 isKeyboardEnabled         | boolean       | true                           | Enable keyboard events (up, down, left, right)
 isOpenBeginning           | boolean       | true                           | Show the beginning of the timeline as open ended
 isOpenEnding              | boolean       | true                           | Show the ending of the timeline as open ended

This is how it can be used.

```
import HorizontalTimeline from 'react-horizontal-timeline-tooltip';

/*
Format: YYYY-MM-DD
Note: Make sure dates are sorted in increasing order
*/
const VALUES = [
    '2008-06-01',
    '2010-06-01',
    '2013-06-01',
    '2015-03-01',
    '2019-01-01',
    '2019-06-17',
    '2019-08-01',
];

const customTooltips = [
    (<div>Tooltip-1</div>),
    (<div>Tooltip-2</div>),
    (<div>Tooltip-3</div>),
    (<div>Tooltip-4</div>),
    (<div>Tooltip-5</div>),
    (<div>Tooltip-6</div>),
    (<div>Tooltip-7</div>),
]

export default class App extends React.Component {
  state = { value: 0, previous: 0 };

  render() {
    return (
      <div>
        {/* Bounding box for the Timeline */}
        <div style={{ width: '60%', height: '100px', margin: '0 auto' }}>
          <HorizontalTimeline
            index={this.state.value}
            indexClick={(index) => {
              this.setState({ value: index, previous: this.state.value });
            }}
            values={ VALUES }
            tooltip={ customTooltips }
        </div>
        <div className='text-center'>
          {/* any arbitrary component can go here */}
          {this.state.value}
        </div>
      </div>
    );
  }
}

```
For more advanced usage take a look at the demos directory.

## Running the development version
- Just clone the repo and do an `npm install` (or `yarn install`)
- Run `npm run start`/`npm start`/`yarn start`.
- Then go to `localhost:5001/demos/<demo_name>/index.html` to see the fruits of your labor.
