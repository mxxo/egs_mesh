# Run the simulation and view the results

To run the simulation, you'll use the `mevegs` EGSnrc user code, which outputs the results to a VTK file to be analyzed in Paraview.

> As an `egs++` geometry, `EGS_Mesh` is technically usable from any `egs++` application. But `mevegs` converts `EGS_Mesh` results to VTK for quick analysis without any extra steps.

Back when you created the mesh file, you also assigned media names. In this example, the only media was `H2O`, but simulations can have many different media. For all mesh media, you have to ensure that EGSnrc has the corresponding data loaded. This can either be done by specifying a `pegs4dat` file using the `-p` flag on the command line, or defining the media in the input file. Either method is fine, but for this example you'll use a `pegs4dat` file. The file `tutor_data.pegs4dat` comes bundled with EGSnrc and has a definition of `H2O`.

Enter the `mevegs` directory in `egs_home` and run the simulation:

`mevegs -i cube.egsinp -p tutor_data.pegs4dat`

Make sure the `cube.msh` file is in the same directory you're running the code in.

EGSnrc will print a few screens of information to the console and then report simulation progress until it's done. 

```text
Running 1000000 histories

  Batch             CPU time        Result   Uncertainty(%)
==========================================================
      1                1.09       0.501526           0.31
      2                2.44       0.501762           0.22
      3                3.70       0.502413           0.18
      4                5.22       0.501949           0.16
      5                7.25       0.501994           0.14
      6                9.19       0.501892           0.13
      7               10.92       0.501821           0.12
      8               13.03       0.501918           0.11
      9               15.42       0.502218           0.10
     10               17.25       0.502418           0.10


Finished simulation

Total cpu time for this run:            17.25 (sec.) 0.0048(hours)
Histories per hour:                     2.08696e+08
Number of random numbers used:          121444161
Number of electron CH steps:            5.88643e+06
Number of all electron steps:           9.2142e+06


 last case = 1000000 Etot = 1e+07


================================================================================
Finished simulation

  Elapsed time:                   20.5 s (  0.006 h)
  CPU time:                       17.8 s (  0.005 h)
  Ratio:                          1.152
```

Afterwards, there should be a new file called `cube.vtk`. Start Paraview and open this file using `File->Open`, and `Apply` in the `Properties` toolbar. Color the mesh by `dose` to see the dose results.

![View the dose results](./cube_dose.png)

And you're done! That's a full `EGS_Mesh` simulation from start to finish. Color the mesh by `uncertainty` to see whether these results can be trusted, or if you need to run more histories to be sure. 

### Going further

1. Refine the mesh and run another simulation. How did the simulation runtime change? Do the results look different? More refined meshes are required to observe accurate dose gradients.

2. After the simulation, the histories per hour is reported. Run a simulation with more histories and check if the histories per hour changes. Given this number, how long would it take you to run one billion histories?

3. Run an `EGS_XYZGeometry` simulation with a similar number of elements and compare the simulation runtimes. Typically, `EGS_Mesh` simulations are 2 to 3 times slower than `EGS_XYZGeometry`. Do you observe this? How do the results compare?

4. The dose result is fairly uneven, especially for coarse meshes like this one. Why? Does this persist if you keep refining the mesh?

### References

* [EGSnrc home page](https://nrc-cnrc.github.io/EGSnrc/)
* [EGSnrc `egs++` library manual](https://nrc-cnrc.github.io/EGSnrc/doc/pirs898/)
* [Gmsh reference manual](https://gmsh.info/doc/texinfo/gmsh.html)
* [Paraview manual](https://docs.paraview.org/en/latest/)
