# Pachinko

A game app that demonstrates various aspects of SpriteKit.  The user is able to use balls that can interact with obstacles that are created by the user themselves and drop them into different slots and gain or lost points depending on the slot.

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/final.png" width="400">

## Features

Comparison of the equivalent features between UIKit and SpriteKit:

| UIKit          | SpriteKit |
| --- | --- |
| Interface Builder | Scene Editor |
| Position based on  top-left corner | Based on the centre |
| Y: 0 means top | Y: 0 means bottom |
| UIImage | SKSpriteNode |
| Screens | Scenes |
| viewDidLoad() | didMove(to: ) |
| UILabel | SKLabelNode |


### SpriteKit

SpriteKit is Apple’s general purpose framework for drawing shapes, text, images, video, and particles in two dimensions.  It’s for creating graphic-intensive apps, whether it be iOS, MacOS, iPadOS, or WatchOS. It uses Metal which is what gives SpritieKit access to the host device’s GPU.  Utilizing GPU will enable the app to achieve the potentials of the graphic-intensive elements the project has to offer.

### SKSpriteNode

SKSpriteNode is similar to UIImage from UIKit.  It can display any images or solid colour.  It’s being used to display the image assets in this project. It comes with a variety of methods to manipulate the image or the solid colour, such as setting the z-position value to bring the image to the foreground or to the background, adjusting the size and the position or the setting blend mode.  

### SKBlendMode 

The blend mode is to determine how the colour of the source is going to be blended into the colour of the destination.  For example, when we add the a SKSpriteNode as a child to the parent node, we need to calculate what the resulting colour of adding these two together.

- alpha: The source and destination colours are blended by multiplying the source alpha value
- add: The source and destination colour are added together
- subtract: The source colour is subtracted from the destination colour
- multiply: The source colour is multiplied by the destination colour
- multiplyX2: The source colour is multiplied by the destination colour and then doubled
- screen: The source colour is added to the destination colour times the inverted source colour
- replace: The source colour replaces the destination colour. 

In this project, we’re using “.replace” since we want to set an image of our choice to replace the destination as the background. 

```
let background = SKSpriteNode(imageNamed: "background")
background.position = CGPoint(x: 512, y: 384)
background.blendMode = .replace
background.zPosition = -1
addChild(background)
```

### SKPhysicsBody

SKPhysicsBody is an object that contains the physics mathematics, such as gravity, friction, mass, etc that can be used out-of-box.  Every node has a property called “physicsBody” that is optional.  When you instantiate the SKPhysicsBody and assign it to the physicsBody property of a node, that particular node will possess certain physics attributes. 

An instance of SKPhysicsBody can be one of two things: a volume-based body or an edge-based body.  A volume-based body could be of any shape with a volume, like a circle, rectangle, trapezoid, etc.  You can instantiate it with the shape, size, or texture, and the node that’s been assigned with the shape will be subject to the gravity, bounce off other nodes, or whatever other attributes you assign. 

The edge-based body’s main purpose is to interact with the volume-based body, but it itself has no mass and is non-solid.  It’s used as a boundary for volume-based bodies could collide against. In this project, the frame of the scene is used as the edge-based body that the squares of volume-based bodies could fall onto.

- Edge-based body:

```
physicsBody = SKPhysicsBody(edgeLoopFrom: frame)
```

The above is so that other physics bodies will recognize the frame of your device’s display as something to be interacted with, namely bounced off of.  
By default, every physics bodies will interact with each other unless otherwise specified. 

- Volume-based body
```
box.physicsBody = SKPhysicsBody(rectangleOf: CGSize(width: 64, height: 64))
ball.physicsBody = SKPhysicsBody(circleOfRadius: ball.size.width / 2)
```
Above is to create a physics body of a ball and a box that’s going to bounce off of. 

### SKAction

SKAction is an object to animate a node in the scene.  It can be used for:
- changing a node’s position and zRotation
- changing a node’s size or scaling properties
- changing a node’s visibility or making it translucent
- changing a sprite node’s contents so that it animates through a series of textures
- colorizing site node
- playing sounds
- removing a node from the node tree
- rotate
        
This project demonstrates the use of SKAction for the rotation animation:

```
let spin = SKAction.rotate(byAngle: .pi, duration: 10)
let spinForever = SKAction.repeatForever(spin)
slotGlow.run(spinForever)
```

### Development Sequence

1. First created square shaped SKSpiriteNode with SKPhysicsBody attribute of the same shape.  Each box is added to the parent at the position where the user taps on the screen.

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/1.png" width="400">

2. Changed the shape of the box from a square into a circle. 

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/2.png" width="400">

3. Added the bouncers in the bottom part of the frame that possess the SKPhysicsBody attributes and are non-dynamic

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/3.png" width="400">

4. Added Slot Base and Slot Glow that are “good” and “bad” to denote where the user can gain or lose points.  SKAction enables the Slot Glow to rotate in a continuous fashion.

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/4.png" width="400">

5. SKLabelNode for displaying the score, toggling the edit mode, and displaying the warning that the ball has to be of certain height are added. The SKEmitterNode to display the fire is also added.

<img src="https://github.com/igibliss00/Pachinko/blob/master/README_assets/5.png" width="400">


