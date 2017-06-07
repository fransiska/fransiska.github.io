---
layout: post
title: Reading accelerometer in iOS app
description: ""
category: iOS
tags: [iOS, game, accelerometer]
date: 2017-06-08 00:12:00 +07:00
---

In XCode, start with `File-New-Project: Game`. This will create a demo project, but we will delete most of it.
Delete `GameScene.sks` and `Actions.sks`. Since the `Spaceship` image is included in the Assets, we will just use it. Move the Spaceship image to the 2x box. We will deal with `GameViewController.swift` and `GameScene.swift` only.

## GameViewController.swift

This is all we have for the GameViewController class in `GameViewController.swift` This sets up the Sprite Kit View, show the frame counts, hides status bar.

```swift
class GameViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let scene = GameScene(size: view.bounds.size)
        scene .scaleMode = .resizeFill
        
        let skView = view as! SKView
        skView.showsFPS = true
        skView.ignoresSiblingOrder = true
        skView.presentScene(scene)
    }
    
    override var prefersStatusBarHidden: Bool {
        return true
    }
}
```

## GameScene.swift

### Initializing `SKScene`

Delete all the content of `GameScene` class. First we want to define the sprite and motion manager to read the accelerometer.

```swift
let player = SKSpriteNode(imageNamed: "Spaceship")
let motionManager = CMMotionManager()
```

We also want to define the variables which stores the x and y position of the sprite. It is of type CGFloat, because that's the type that's used to update the position of the sprite, not Int or Double.

```swift
var posx:CGFloat = 0
var posy:CGFloat = 0
```

To put on the sprite on the screen, we call `addChild` in `didMove`. We also specify the initial position of the sprite. This is called (once) when the scene is presented into the `SKView`.

```swift
override func didMove(to view: SKView) {
    backgroundColor = SKColor.black
    posx = size.width/2
    posy = size.height/2
    player.position = CGPoint(x: posx, y: posy)
    addChild(player)
}
```

### Handling accelerometer updates

In the same function, we want to connect the data updates from the motion manager to a function which crunches it. We need to check if the device has accelerometer. We then ask the motion manager to start sending the updates and put it in a queue. The updates are put into the `deviceMotion` variable. If there is no error, the updates will trigger the function `handleDeviceMotionUpdate`, which we define below.

```swift
if motionManager.isDeviceMotionAvailable {
    motionManager.startDeviceMotionUpdates(to: OperationQueue.current!, withHandler: {
        (deviceMotion, error) -> Void in
        if(error == nil) {
            self.handleDeviceMotionUpdate(deviceMotion: deviceMotion!)
        }
    })
}
```

This function below will be called each time there is an update in the accelerometer values. It receives the `deviceMotion`. The roll, pitch, yaw values can be accessed by `deviceMotion.attitude.roll` and so on.

```swift
//handle accelerometer values updates
func handleDeviceMotionUpdate(deviceMotion:CMDeviceMotion) {
    let attitude = deviceMotion.attitude
    //saves attitude.roll as roll, etc.
    movePlayer(roll: roll, pitch: pitch)
}
```

Another function handles how we want to move the sprite. After updating the positions, we finally set the position of the sprite by setting its `position` to a `CGPoint(x: Double, y:Double)`.

```swift
func movePlayer(roll: Double, pitch: Double) {
     if(roll < 0) {
         posx -= 5
     }
     //do more position updates

     //sets the sprite position
     player.position = CGPoint(x: posx, y: posy)
}
```

That's it! The sprite will be refreshed accordingly in the new frame! I put the whole project in [my git](https://github.com/fransiska/swiftAccelerometerBasic).

source: [forestgiant](https://www.forestgiant.com/articles/ios-core-motion/) and [ioscreator](https://www.ioscreator.com/tutorials/move-sprites-accelerometer-spritekit-swift)

