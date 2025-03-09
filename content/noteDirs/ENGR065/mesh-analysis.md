+++
date = '2025-03-08T20:34:15-08:00'
draft = false
title = 'Mesh Analysis'
+++

Mesh analysis is a circuit analysis method that attempts to decrease the total number of equations needed to solve a 
circuit. Mesh analysis only works on **planar** circuits. 

A **planar circuit** is a circuit that can be drawn on a plane with no wires crossing each other

### steps:
1) Find and label all meshes. A mesh is a closed loop that does not contain any other loops within it
2) Assume a clockwise current in each mesh/loop
3) Use KVL in each loop; use Ohm's law if necessary
4) Solve the system of equations

### supermesh
If there is a current source in between two meshes, we call that a super mesh. We can 'remove' the supermesh and treat 
the two loops as one loop. We make one big equation. We will also make another equation relating the current source to
the two mesh currents

### dependant sources
We will need an additional equation to deal with a dependant voltage source.
