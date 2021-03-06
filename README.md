Python implementation of Tarjan's algorithm
===========================================

Tarjan's algorithm takes as input a directed (possibly cyclic!) graph and
returns as output its strongly connected components in a topological order.

Example
-------
![](http://github.com/bwesterb/py-tarjan/raw/master/doc/example.png)

```python
>>> tarjan({1:[2],2:[1,5],3:[4],4:[3,5],5:[6],6:[7],7:[8],8:[6,9],9:[]})
[[9], [8, 7, 6], [5], [2, 1], [4, 3]]
```

Uses
----
### Cyclic dependencies
In various cases, dependencies might be cyclic and a group of interdependant
actions must be executed simultaneously.  It is not uncommon that
the simulataneous execution is costly.  With Tarjan's algorithm, one can
determine an efficient order in which to execute the groups of interdependant
actions.

### Transitive closure
Using Tarjan's algorithm, one can efficiently compute the transitive
closure of a graph.  (Given a graph _G_, the transitive closure of _G_
is a graph that contains the same vertices and contains an edge from _v_
to _w_ if and only if there is a path from _v_ to _w_ in _G_.)

The transitive closure is implemented in `tarjan.tc`:

```python
>>> tc({1:[2],2:[1,5],3:[4],4:[3,5],5:[6],6:[7],7:[8],8:[6,9],9:[]})
{1: (1, 2, 5, 6, 7, 8, 9),
 2: (1, 2, 5, 6, 7, 8, 9),
 3: (3, 4, 5, 6, 7, 8, 9),
 4: (3, 4, 5, 6, 7, 8, 9),
 5: (8, 9, 6, 7),
 6: (8, 9, 6, 7),
 7: (8, 9, 6, 7),
 8: (8, 9, 6, 7),
 9: ()}
```

### Expand group hierarchies
Given a graph of groups, one can use the transitive closure to determine
all indirect members of a group.  (Someone is an indirect member of a group,
if it is a member of a group that is a member of a group that ... is a member
of the group.)

Installation
------------
Simply execute

    easy_install tarjan

or from this source distribution, run

    python setup.py install
