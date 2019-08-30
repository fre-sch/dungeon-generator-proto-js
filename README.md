# dungeon-generator-proto-js

Each room is a byte, using each bit as connection feature in one of the
cardinal directions (north, east, south, west) `WWSSEENN`.
A Connection feature is either a door, or an open wall. Doors are stored in
odd bits, walls are stored in even bits `WDWDWDWD`.

At a given position, generate a random byte value, where either a door bit or
a wall bit is set, but not both. No random value is generated, if given
recursion depth has been reached. Recursion ends because there's no new
opening feature from random, a room already exists, or next room position will
be out of bounds.

Scan around the current position for existing
rooms and merge their connection features, such that the current room contain
the opposing feature. If the room to the south has a north door, enable the
south door for the current room, connecting both rooms. If the west door has
no east door or open wall, disable the west door or west wall in the current
room.

Add the room to the grid at the given position.

Scan around the given position again. If there is a connection feature in the
current room for the cardinal direction, and not already a room present, or out
of bounds, recurse with the next position, passing along the previous
connection feature. The next recursion will use the opposing feature of the
previous feature, ie if passed a west door the next room will include an east
door.
