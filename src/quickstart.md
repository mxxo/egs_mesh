# EGS_Mesh

`EGS_Mesh` is a general-purpose unstructured tetrahedral mesh library for [EGSnrc](https://nrc-cnrc.github.io/EGSnrc/).

`EGS_Mesh` offers increased modelling flexibility over traditional voxel-based simulations. Instead of building up a geometry using a constructive-solid approach, `EGS_Mesh` takes a tetrahedral mesh file as input. Geometries created in CAD can be meshed and then simulated directly. `EGS_Mesh` relies on the standalone tool [Gmsh](https://gmsh.info/) to generate meshes.

## Examples

### Basic input file syntax
```text
:start geometry description:
    :start geometry:
        library = egs_mesh
        name = my_mesh
        file = model.msh     # your mesh here
    :stop geometry:

    simulation geometry = my_mesh
:stop geometry description:
```

### In an envelope
```text
:start geometry definition: 
    :start geometry:        
        library = egs_mesh
        name = my_mesh    
        file = model.msh 
    :stop geometry:

    # define a 50cm air cube at the origin
    :start geometry:
        library = egs_box
        name = my_box
        box size = 50 50 50
        :start media input:
            media = air
        :stop media input:
    :stop geometry:
    
    # embed the mesh in the air box
    :start geometry:
        library = egs_genvelope
        name = my_envelope
        base geometry = my_box
        inscribed geometries = my_mesh
    :stop geometry

    simulation geometry = my_envelope
:stop geometry definition:
```

## Alternatives 
Other Monte Carlo codes that support tetrahedral mesh simulations include:
* [Geant4](https://geant4.web.cern.ch/) 
* [MCNP6](https://mcnp.lanl.gov/)
* [PHITS](https://phits.jaea.go.jp/)
