# Mars Rover Kata

You’re part of the team that explores Mars by sending remotely controlled
vehicles to the surface of the planet. Develop an API that translates the
commands sent from Earth to instructions that are understood by the rover.

Note: This is not an original Kata by me, see provenance section to see its origins.

## A Moving Rover

You are given the initial starting point (x,y) of a rover and the direction
(N,S,E,W) it is facing.

An example position might be 0, 0, N, which means the rover is in the bottom
left corner and facing North. Assume that the square directly North from (x, y)
is (x, y+1), and that the square directly East from (x, y) is (x + 1, y).

The rover receives a character array of commands.

Implement commands that move the rover forward/backward (F,B).

Implement commands that turn the rover left/right (L,R).

### Test input 1

Given a rover at position:

```
1 2 N
```

and the movement sequence:

```
LFLFLFLFF
```

we expect the rover to be at

```
1 3 N
```

### Test input 2

Given a rover at position:

```
3 3 E
```

and the movement sequence:

```
FFRFFRFRRF
```

we expect the rover to be at:

```
5 1 E
```

## Challenges

Work through these for some extra challenges; pick the ones you like.

### Obstacle detection

The surface of Mars contains obstacles, and the rover shouldn't go over it.

As a safety measure, implement obstacle detection before each move to a new
square. If a given sequence of commands encounters an obstacle, the rover moves
up to the last possible point, aborts the sequence and reports the position of
the the obstacle.

Implement obstacle detection planning. If a given sequence of commands would
cause the rover to go over an obstacle, have the rover report on the position
of the offending obstacle without moving.

### Idea: obstacle shapes

Implement obstacles of more complicated shapes.

### Display

Implement a simple text display showing the position of rovers and obstacles,
centered around some coordinate. Mark rovers with R and obstacles with O; empty
grid squares are the space character.

### Fancy Display

Create a legend for the display, explaining the various objects (O and R).

Create a coordinate system indication in the margins:

```
5



0
 12   17
```

Make it so that the display updates for each time step so you can watch runs
live.

### Multiple rovers

Implement multiple rovers. A rover counts as an obstacle.

Only one rover moves at the time.

### Simultaneous movement

Rovers now all start moving at the same time. They are each given their own
movement sequence, and execute steps one after another. They can be assumed to
take turns in a consistent order. Rovers still count as obstacles, so make sure
that at least the safety feature works correctly.

## Provenance

This kata is unusual in that it has multiple versions around, each with
slightly different requirements. Some have multiple rovers, some have wrapping
at the edges, some allow the rover to go backwards, and some have obstacle
detection. I've made a selection of what I thought was interesting and added a
few challenges of my own. The oldest version appears to be:

https://code.google.com/archive/p/marsrovertechchallenge/

Here are some more varieties:

https://kata-log.rocks/mars-rover-kata

https://danilsuits.github.io/mars-rover-kata/
