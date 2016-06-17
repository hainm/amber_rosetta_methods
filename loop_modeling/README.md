- Generate topology and resart files for AMBER minimization

    ```bash
    export root_dir=/project1/dacase-001/haichit/rosseta_amber/loop_modeling/
    export pdb_folder=1oyc
    python scripts/generate_rst7_parm7_files.py $pdb_folder $root_dir

    # $pdb_folder: a new $pdb_folder will be created in this current folder
    # $root_dir: where you have all original pdb files

    # This script will create a $pdb_folder in this current dir
    # and generate AMBER's topology and restart files for minimization.
    # For demonstration, I only kept:
    #     1oyc.1oyc_1oyc3476_0001.parm7
    #     NoH_1oyc_1oyc3476_0001.pdb
    #     NoH_1oyc_1oyc3476_0001.rst7
    ```

- Run minimization
    
    ```bash
    cd 1oyc
    python ../scripts/run_min.py -p 1oyc.1oyc_1oyc3476_0001.parm7 \
           -O -c "NoH*.rst7" -i ../input/min.1oyc.in

    # minimized coordinate filename: min*rst7
    # Make sure to update the loop mask in min.1oyc.in if you work with another protein code
    ```

- Compute AMBER potential energy

    ```bash
    python scripts/eamber_single.py 1oyc

    # '1oyc/min_NoH_1oyc_1oyc3476_0001.rst7', -14104.493621118669 (kcal/mol)
    ```

Methods
-------
- Minimization were performed using 14SBonlysc force field and GBNeck2 implicit solvent model.
XMIN method is used with max cycles of 1000. Minimization will be stopped if the root-mean-square
of the Cartesian elements of the gradients is less than 0.01 kcal/mol. The heavy atoms of non-loop region were
restrained with restraint force constant of 10.0 (kcal/mol-Å^2)

All minimization and energy evaluations were performed with the sander and its Python interface `pysander`
program in development version of [AmberTools16](
http://ambermd.org/AmberTools16-get.html)
