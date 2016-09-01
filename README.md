# A React Roman numeral converter 

## Breakdown of my react component
First I create a new react component with an inititial state of no user input.
```javascript
var Input = React.createClass({
  getInitialState: function () {
    return {userInput: ""};
  });
```
Next I add the function to handle the event of user input.
```javascript
var Input = React.createClass({
  getInitialState: function () {
    return {userInput: ""};
  },
  handleUserInput: function (e) {
    this.setState({userInput: e.target.value})
  });
```
This is my roman numeral converter, I just threw it in the component to work. Probably a better way to do this but it works.
```javascript
  toRoman: function(numString) {
    var nums = { 1000:'M', 900:'CM', 500:'D', 400:'CD',100:'C', 90:'XC', 50:'L', 40:'XL', 10:'X',9:'IX', 5:'V', 4:'IV', 1:'I' }
    var result = "";
    var keys = Object.keys(nums);
    var i = keys.length - 1;

    while(i >= 0) {
      var int = keys[i]
      while(numString >= parseInt(int)) {
        numString -= int;
        result += nums[int];
      }
      i--;
    }
    return result
  }
```
And lastly, my render function. I bind the `handleUserInput` function to an `onChange` event on my input element.
Then I pass that input through my `toRoman` function and display it in the `<h1>` tags.
```javascript
render: function () {
  return (
    <div id="container">
      <input type="text"
             onChange={this.handleUserInput}
             value={this.state.userInput}
             maxLength="5" />
      <div id="roman">
        <h2>Roman Numeral</h2>
        <h1>{this.toRoman(this.state.userInput)}</h1>
      </div>
    </div>
  );

```
### Finally the whole thing
```javascript
var Input = React.createClass({
  getInitialState: function () {
    return {userInput: ""};
  },
  
  handleUserInput: function (e) {
    this.setState({userInput: e.target.value})
  },
  
  toRoman: function(numString) {
  var nums = { 1000:'M', 900:'CM', 500:'D', 400:'CD',100:'C', 90:'XC', 50:'L', 40:'XL', 10:'X',9:'IX', 5:'V', 4:'IV', 1:'I' }
  var result = "";
  var keys = Object.keys(nums);
  var i = keys.length - 1;

  while(i >= 0) {
    var int = keys[i]
    while(numString >= parseInt(int)) {
      numString -= int;
      result += nums[int];
    }
    i--;
  }
  return result
},

render: function () {
  return (
    <div id="container">
      <input type="text"
             onChange={this.handleUserInput}
             value={this.state.userInput}
             maxLength="5" />
      <div id="roman">
        <h2>Roman Numeral</h2>
        <h1>{this.toRoman(this.state.userInput)}</h1>
      </div>
    </div>
  );
}
});
```
