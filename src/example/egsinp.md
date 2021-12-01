# Write an egsinp file

Now, you're ready to make a new simulation input file. The three required input file sections are:

1. Geometry definition
2. Source definition 
3. Run control

First up, let's define the mesh geometry. An `EGS_Mesh` geometry block looks like:

```text
:start geometry definition:
    :start geometry:
        library = egs_mesh
        name = my_mesh
        file = cube.msh # your mesh here
    :stop geometry:
    simulation geometry = my_mesh
:stop geometry definition:
```

The only input we need to adjust is the mesh `file`. If you're following the guide, this file should be called `cube.msh`.

Next, the source. Let's define an exterior point source. The meshed box starts at the origin and extends 10cm along `x`, `y` and `z`. So placing the source at `(5, 5, -1)` means the source will be 1cm away from the box's `-z` face. We'll simulate a 10MeV photon monoenergetic point source.

```text
:start source definition:
    :start source:
        library     = egs_point_source
        name        = my_source
        position    = 5 5 -1
        :start spectrum:
            type    = monoenergetic
            energy  = 10
        :stop spectrum:
        charge      = 0
    :stop source:
    simulation source = my_source
:stop source definition:
```

And finally, the run control section. Let's run 1 million histories.
```text
:start run control:
    ncase = 1e6
:stop run control:
```

The input file is done, and you're ready to [run the simulation](./run_sim.md).
```text
:start geometry definition:
    :start geometry:
        library = egs_mesh
        name = my_mesh
        file = cube.msh
    :stop geometry:
    simulation geometry = my_mesh
:stop geometry definition:

:start source definition:
    :start source:
        library     = egs_point_source
        name        = my_source
        position    = 5 5 -1
        :start spectrum:
            type    = monoenergetic
            energy  = 10
        :stop spectrum:
        charge      = 0
    :stop source:
    simulation source = my_source
:stop source definition:

:start run control:
    ncase = 1e6
:stop run control:
```
