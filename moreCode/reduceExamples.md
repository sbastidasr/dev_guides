```txt
Mark Johannson  blender  200  1
Mark Johannson  iron 80  2
Sarah Smith   kitchen 20 1
```

```javascript
import fs from 'fs'

var output =  fs.readFileSync('data.txt','utf8')
  .trim() //deletes whitespace at the end
  .split('\n') //splits into an array. One object per line.
  .map(line = line.split('\t')) //maps each line into array:
  .reduce((customers, line) => {
    customers.[line[0]]=customers.[line[0]] || [];
    customers.[line[0]].push({
      name:line[1],
      price:line[2],
      quantity:line[3]
    })
    return customers
  }, {}) //empty starting object.

console.log('output', JSON.stringiify(output,null,2))
```
