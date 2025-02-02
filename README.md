# omni_shapes
Let's try to find Omni Shapes or Polyominoes!
---
<sub>What started off as a new rule or two that could be used to define how to make Polyominoes, turned into slowly building a websoft to just find Omni Shapes (or Polyominoes) in 
 a slightly <i>new way</i></sub>

</br></br>
&nbsp; &nbsp; To start, The major thing Omni Shapes does different then Polyominoes is tracking the shapes by relatable coordinates instead of visual or matrix based methods. Ideally, we would place our first block in the relatable spot on the graph as to the first block we plan on taking (not placing) then we can track each block's position and backtrack to determine the possible numbers "taken" even after a push (to ensure we don't break the take-place rule used to determine finding Polyominoes). For example if we always place the smallest number at the top of 1st placed block & if I know I'm going to pick the right side block of the first, then I'll place the first block at 4,4 (scale out as your dimensions rise ie: 4,4,4 [3D] && 4,4,4,4 [4D]). Now any move we make we can record the difference from the previous position to the current and this will allow us to track each step. When recording, lead by placing the starting postion then within brackets the changes and outside the brackets the tailing end should be the ending location. This should allow anyone to be able to grab a graph and re-create the shape, also this allows us to find Omni Shape reflections or "free" Polyominoes. A simple reflection is just the opposite sign of the change but we could use an algo to find all free shapes or omni reflections.</br></br>&nbsp; &nbsp; Because we are using corridanates we can take each position of the blocks (by starting at the start and working down the changes to the end) and mathematically or deterministically rotate based on the grid (like rotating a block that has a specific shape on it) <code>((max-grid-size MINUS grid-position-per-plane) PLUS one)</code> but also we can just flip the X-Y values to create a mirror and in higher deminsions flipping the alpha & delta with x & y should flip the shape inside-out. Now without folding symatry methods nor heavy matrix maths we can find all the Omni's reflections (or "free Polyominoes").</br>&nbsp; &nbsp; Shapes are their specific pattern in their change arrays. For example: in each change array (x|y|alpha|delta|[...]) we have start[change]end. A real 2D Omni may look like <code>4[-1,-1,0]2;4[0,0,1]5</code>. It's an "L" type shape that moves 2 times in one direction then moves 90deg off one side for one block, making the total length 4 (or L4). Started at 4,4 ended at 2,5. So the pattern <code>(A,A,B):(B,B,A)</code> is a specific shape and we can then use this as a changeable object. As we find more Fixed Polyominoes or Unique-Patterned Omnis we can hot swap sections with these shape patterns while keeping true to the object before it. If need be we can always do test pushes to see if an addtional set of onjects can be placed around the edges of the object (to detect self & patterns looping around to have holes). Just push for as many times your longest length of the shape is or the length of the non-null objects of the change array with the most non-null objects.
</br></br>&nbsp; &nbsp; At the moment the Omni Shape Finder doesn't do all the extra steps to finding new moves nor does it use the simple method described above. It's easier to start at Null (0) and change by (0) then build patterns then hot swap the patterns with slow rising changing numbers and slowly rising the length as you find all patterns within a length. Instead the Omni Shape Finder uses video game logic to "look" around and find potential moves, records them then tries to send a clone in it's place to take that potential move.


Example Omni:
</br>
X Plane: <code>4[0,0,0,-1,-1,0,0,0,-1,0,0,0,0,0,1,1,1,1,1,1,1,1,0,0,0,0,0,0,-1]8</code></br>
Y Plane: <code>4[-1,-1,-1,0,0,1,1,1,0,1,1,1,1,1,0,0,0,0,0,0,0,0,-1,-1,-1,-1,-1,-1,0]3</code></br>
Z Plane (alpha): <code>4[1,1,0,0,0,-1,0,0,0,0,1,0,0,0,0,0,0,-1,-1,-1,-1,-1,0,0,0,1,1,0,0]3</code></br>

3D Omni Shape Mapped: </br>(</code>4[0,0,0,-1,-1,0,0,0,-1,0,0,0,0,0,1,1,1,1,1,1,1,1,0,0,0,0,0,0,-1]8;4[-1,-1,-1,0,0,1,1,1,0,1,1,1,1,1,0,0,0,0,0,0,0,0,-1,-1,-1,-1,-1,-1,0]3;4[1,1,0,0,0,-1,0,0,0,0,1,0,0,0,0,0,0,-1,-1,-1,-1,-1,0,0,0,1,1,0,0]3</code>)</br>
</br>
That would be a real 3D Polyomino with 30 blocks (or an L30 Omni)! 
</br>
</br></br>
Next, I want Omni Shapes to find & make additional pushes avaiable (after the inital algo-push/move) until it's found potientially all shapes per length as the user is clicking to build their Omni Shape. Eventually, I'll probably do the simple line algo across multiple planes (x|y|alpha|delta|[...]) to then mix and match shapes after finding the simplist 13 shapes. Most likely I'll use the tricks I used with [SPX](https://github.com/digimancer3d/spx) to help make that happen.  &nbsp;  ;}
</br></br>
Try Omni Shapes (websoft) vis-a-vis gisthub preview: [3dd.in/Omni](https://3dd.in/Omni)

</br></br>

For anyone whom wants to try the simplified array-attack method for finding Omnis, please try the "Simple Omni Game" HTML file.
</br>
</br></br><hr>

&nbsp; <i>3D's Note:</br>&nbsp; &nbsp; <b>The Simple Omni Game method has many bugs so the most recent version has not been updated. I am making explination images to help reconfigure the maths and checks to get the array pairing working up to 3 dimensions. I was wanting to go beyond 3 dimensions and found a syncing bug that happens in some higher dimension formats because of the current paring bug. Next will be images and hopefully eventually a rule set to help others find more Omni Shapes which are just a different way to look at Polyominoes! (The name Omni comes from me unable to say "Polyomino" so when I attempt to say the same word it comes out, "Poly-Omni-O", but I continued to call them Omni Shapes as I discovered these "Between Complexity Topologies" (my perspective on what are Polyominoes) can create almost any shape. Now that I've made the frist few images, I have discovered why the syncing happens. Arrays within arrays may sync if the external array has only one sign or flips-flops signs in a consistent pattern. This does mean that an internal dimension like the 4th, 5th & 6th dimensions are going to have to track something other than object placement. For example, using the delta or alpha-plane (which is the distance from you) tracks the amount of light difference upon a location as well as if it is null or not. Another example is the 4th dimension tracks the number of touching boxes including if it is null or not. These have to be done in a single digit or decimaled-digit but I believe there should be a single digit solution to the dualities of differences (what we are tracking in the array-based method).</b></i>
</br><hr></br></br>

# Omni Shape Rules & Explinations

</br></br>

&nbsp; &nbsp; Proof digits are used to track to the open sides during the time of selecting a new block to be placed, but this also limits where future blocks can be placed since we cannot take a proof digit lower than the previous taken proof digit. This is not a unique rule, it is the Polyomino base rule.

&nbsp; &nbsp; Other rules may be usable depending on if the array is paired or not.


</br></br></br>

### Single Array Explination (img):

![Single Array Explination](https://raw.githubusercontent.com/DigiMancer3D/omni_shapes/refs/heads/main/Visuals/Single%20Array%20Movement%20Explination.png)

</br></br>

### Paired Array Explination (img):

![Paired Array Explination](https://raw.githubusercontent.com/DigiMancer3D/omni_shapes/refs/heads/main/Visuals/Paired%20Array%20Movement%20Explination.png)

</br></br>

### Tri-Paired Array Explination (img):

![Tri-Paired Array Explination](https://raw.githubusercontent.com/DigiMancer3D/omni_shapes/refs/heads/main/Visuals/Tri-Paired%20Array%20Movement%20Explination.png)





