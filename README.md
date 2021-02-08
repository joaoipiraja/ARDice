[<img src="/ARDice/Assets.xcassets/AppIcon.appiconset/120.png"/>](120.png)
# ARDice
Dice IOS Virtual Reality App using ARKit/Swift 5.3
### Learn 📝
#### Rotate Animation
```Swift
func roll(dice:SCNNode){
        let randomX = Float(arc4random_uniform(4)+1)*(Float.pi/2)
        let randomZ = Float(arc4random_uniform(4)+1)*(Float.pi/2)
        
        dice.runAction(
            SCNAction.rotateBy(x: CGFloat(randomX * 5),
                               y: 0,
                               z: CGFloat(randomZ * 5),
                               duration: 0.5)
        )
    }
```
#### Show the dice when the surface is touched
```Swift
 override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        
        
        if let touch = touches.first{
            let touchLocation = touch.location(in: sceneView)
            let results = sceneView.hitTest(touchLocation, types: .existingPlaneUsingExtent)//convert a 2D point to 3D
            
            if !results.isEmpty{
                print("touched the plane")
            }else{
                print("touched somewhere else")
            }
                        
            if let hitResult = results.first{
                print(hitResult)
                let diceScene = SCNScene(named: "art.scnassets/dice.scn")!;
                if let diceNode = diceScene.rootNode.childNode(withName: "Dice", recursively: true){
                    diceNode.position = SCNVector3(x: hitResult.worldTransform.columns.3.x,
                                                   y: hitResult.worldTransform.columns.3.y + diceNode.boundingSphere.radius/100,
                                                   z: hitResult.worldTransform.columns.3.z)
                    
                    diceArray.append(diceNode)
                    sceneView.scene.rootNode.addChildNode(diceNode)
                
                }
            }
            
            
        }
    }
```

### Screenshots 📸
[<img src="/screenshots/screenshot1.png" width="500" />](screenshot1.png)
