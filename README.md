# Generate Random String

A script to generate a random string of any length optionally including upper- and lowercase characters, numbers or selected special characters

# Version 

1.0 Initial

# Global Script Setup
1. Create a Global Script called "GenerateRandomString"
2. Add the input parameters below to the Global Script
   1. Length
   2. Lowercase
   3. Numbers
   4. Special
   5. Uppercase
3. Add the output parameter below to the Global Script
   1. Result
4. Drag a *JavaScript* action into the script
5. Add the Javascript below into the JavaScript code property
```javascript
/* Stadium Script Version 1.0*/
let lengthParameter = ~.Parameters.Input.Length;
if (isNaN(parseFloat(lengthParameter))) lengthParameter = 12;
let lowercaseParameter = ~.Parameters.Input.Lowercase;
if (lowercaseParameter) lowercaseParameter = true;
let numbersParameter = ~.Parameters.Input.Numbers;
if (numbersParameter) numbersParameter = true;
let uppercaseParameter = ~.Parameters.Input.Uppercase;
if (uppercaseParameter) uppercaseParameter = true;
let specialParameter = ~.Parameters.Input.Special;
if (specialParameter) specialParameter = true;

let d = {length: lengthParameter, numbers: numbersParameter, uppercase: uppercaseParameter, lowercase: lowercaseParameter, special: specialParameter};
let result = '';
let uppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
let lowercase = 'abcdefghijklmnopqrstuvwxyz';
let numbers = '0123456789';
let special = '~!@#$%^&*()_-+={]}[|]:;<,>.?/}';

let characters = '';
if (d.uppercase) characters += uppercase;
if (d.lowercase) characters += lowercase;
if (d.numbers) characters += numbers;
if (d.special) characters += special;
const charactersLength = characters.length;
let counter = 0;
characters = sortArrayRandomly(characters.split(""));
characters = characters.join("");
while (counter < d.length) {
  result += characters.charAt(Math.floor(Math.random() * charactersLength));
  counter += 1;
}
return result;

function sortArrayRandomly(d) {
  let currentIndex = d.length,  randomIndex;
  while (currentIndex > 0) {
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;
    [d[currentIndex], d[randomIndex]] = [
      d[randomIndex], d[currentIndex]];
  }
  return d;
}
```
6. Drag a *SetValue* action into the Global Script and place it under the *JavaScript* action
   1. Target: = ~.Parameters.Output.Result
   2. Value: = ~.Javascript

![](images/Parameters.gif)

## Usage
1. Drag the script called "GenerateRandomString" into a script or event handler
2. Enter values for the script input parameters
   1. Length: Integer (default: 12)
   2. Lowercase: Boolean (default: false)
   3. Numbers: Boolean (default: false)
   4. Special: Boolean (default: false)
   5. Uppercase: Boolean (default: false)
