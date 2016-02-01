MurderRobot
 .drive()
 .kill()

 Animal
  .poop()
    Dog
     .bark()

But what if we want a murderRobotDog? then we need composition

dog            = pooper + barker
murderRobotDog = driver + killer + barker


```javascript
const barker = (state) => ({
  bark: () => console.log('Woof, I am ' + state.name)
})
const driver = (state) => ({
  drive: () => state.position = state.position + state.speed
})

const murderRobotDog = (name)  => {
  let state = {
    name,
    speed: 100,
    position: 0
  }
  return Object.assign(
        {},
        barker(state),
        driver(state),
        killer(state)
    )
}
const bruno =  murderRobotDog('bruno')
bruno.bark() // "Woof, I am Bruno"
```
