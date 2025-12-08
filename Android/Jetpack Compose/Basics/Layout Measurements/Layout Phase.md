`layout` lambda accepts a lambda with 2 parameters 
- `measurable` - a list of objects representing children to be laid out that has been measured and can now be placed on screen 
- `constraints` - These are passed down from parents 

- Compose layout system is based on **single pass measurement and layout** model. 
- This method is efficient and preventing infinite loop or inconsistency that can arise from multiple pass system 

## How compose measures and lay out children
 Layout phase is in 2 distinct phase 
 1. Measurement Phase 
 2. Layout Phase 
### Measurement Phase 
Depth First 
- Parent node dictates the constraints to its children 
- Child measure itself within these constraints and report its measure size to the parent.
- This process happens recursively down to composable tree.
- A child cannot know its size until all of its children have measures themselves 
Note - A child can be only be measured once & the parent cannot measure child more than once in a single layout pass.  
This means that layout element will not measure children more than once in order to try different configuration. 
### Layout Phase 
Post order traversal 
- Once the parent knows the measurement for all of its children then it determines the final position (x and y coordinates) for each child relative to itself.
- The parent call **placement** function for each child to place it on the screen 
- This also happens recursively up to tree from bottom most child to root.

``` kotlin 
@Composable 
fun FlowRow(
	modifier: Modifier = Modifier, 
	content: @Composable () -> Unit 
) {
	Layout (
		modifier = Modifier, 
		content = content, 
		measurePolicy = { measurable, constraints -> 
			val placeable = measureable.map { it.measure(constraints) }
			
			val groupedPlaceable = mutableListOf<List<Placeable>>()
			var currentGroup = mutableListOf<Placeable>()
			var currentGroupMaxWidth = 0 
			
			placeable.forEach { placeable -> 
				if(currentGroupMaxWidth + placeable.width >
					constraints.maxWidth) {
					groupedPlaceable.add(currentGroup)
					currentGorup = mutableListOf(placeable)
					currentGroupMaxWidth = placeable.width 
				} else {
					currentGroup.add(placeable)
					currentGroupMaxWidth += placeable.width 
				}
			}
			
			if(currentGroup.isNotEmpty()) {
				groupedPlaceable.add(currentGroup)
			}
			
			layout(
				width = constraints.maxWidth, 
				height = constrains.maxHeight
			) {
				var yPosition = 0
				groupedPlaceable.forEach { row -> 
					row.forEach {
						p.place(
							x = xPosition, 
							y = yPosition, 
						)
						xPosition += p.width
					}
					yPosition += row.maxOfOrNull { it.height } ?: 0 
				}
			}
		}
	)
}


@Composable
fun MyFlowRow() {
	FlowRow {
		repeat(3) {
			Box(
				modifier = Modifier
				.width(Random.nextInt(50, 200).dp)
				.height(100.dp)
				.background(Color(Random.nextLong(0xFFFFFFFF)))
			)
		}
	}
}
```