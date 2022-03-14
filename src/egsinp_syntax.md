# Egsinp syntax

The basic `EGS_Mesh` input file syntax is:

```text
:start geometry definition:
    :start geometry:
        library = egs_mesh
        name = my_mesh
        file = model.msh # your mesh here
    :stop geometry:

    simulation geometry = my_mesh
:stop geometry definition:
```

This example embeds a mesh inside an air box. 

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
    :stop geometry:

    simulation geometry = my_envelope
:stop geometry definition:
```

<!---
This example translates the mesh 5cm along the x-axis:
```
:start geometry definition: 
    :start geometry:        
        library = egs_mesh
        name = my_mesh    
        file = model.msh 
    :stop geometry:

    :start geometry:
    :stop geometry:

    simulation geometry = my_translated_mesh
``` 
-->
