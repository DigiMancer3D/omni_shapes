# omni_shapes
Let's try to find omni shapes or Polyominoes!
---

What started off as a new rule or two that could be used to define how to make Polyominoes, turned into slowly building websoft to find more Omni Shapes (or Polyominioes, idk how to spell the word).


We didn't take away any rules for finding Omni Shapes but instead we are including a "push" concept for finding additional shapes outside what the user has found from clicking. So when we have a defined length, we can push the "loose blocks" around. A loose block is a block touching another blocks face and could be pushed to another face side of the same block without interacting with other blocks after the push.

The only thing different Omni Shapes do outside of Polyominoes (or Polyominioes) is we track the shapes by relatable coordinates. Ideally, we would place our first block in the relatable spot on the graph as to the first block we plan on taking (not placing) then we can track each block's position and backtrack to possible numbers "taken" even after a push (to ensure we don't break the take-place rule).

So our trackers are X[change from previous X,change from previous X,[...]]final-x-position && Y[change from previous Y,change from previous Y,[...]]final-y-position, this let's us see the moves we can recreate the moves if needed but because we allow both positive and negative numbers in the change from previous position we can technically see "up, down, left, right" depending on the change of the value number based on the previous value recrded.

Next, I want Omni Shapes to find additional pushes avaiable until it's found potientially all shapes per Length as the user is clicking to build their Omni Shape.

Try Omni Shapes (websoft) vis-a-vis gisthub preview: [3dd.in/Omni](https://3dd.in/Omni)
