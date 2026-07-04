It is used when size of child is necessary to determine if the another child should be composed or not or to calculate the constraints for other children.

## Example 
- Scaffold needs to determine the size of top bar and bottom bar  first, to calculate the remaining space for main content.  
- The main content is only composed after the bar height are known. 
### Process
1. Phase 1 - Measure the top and bottom bar 
2. Phase 2 - Calculate the content area 
3. Phase 3 (`subcompose`) - Compose and measure the content within calculated constraints

## Code Example
Collapsing header 
