- Generate topology and resart files for AMBER minimization

    ```bash
    export root_dir=/project1/dacase-001/haichit/rosseta_amber/pdz/PDZ_ddG/results/refine/
    export pdb_folder=1be908_wt
    python scripts/generate_rst7_parm7_files.py $pdb_folder $root_dir

    # $pdb_folder: folder that have all original pdb files
    # $root_dir: where you have $pdb_folder 
    # This script will create a $pdb_folder in this current dir
    # and generate AMBER's topology and restart files for minimization.
    # For demonstration, I kept only a single pdb file, rst7 and prmtop in ./1be908_wt folder
    ```

- Run minimization
    
    ```bash
    cd 1be908_wt
    python ../scripts/run_min.py -p prmtop -c "NoH*.rst7" -i ../input/min.in

    # minimized coordinate filename: min*rst7
    ```

- Get AMBER ddG by running MMGBSA method
   
    ```bash
    cd 1be908_wt
    mkdir mmgbsa
    cd mmgbsa
    python ../../scripts/run_mmgbsa.py

    # ddG.csv file will be created

    # Expectation: AMBER's ddG (kcal/mol) for demo snapshot
    # min_NoH_9_2_9_9_repacked_wt_round_2_0020.rst7: -63.18075344
    ```

Methods
-------
- Minimization were performed using 14SBonlysc force field and GBNeck2 implicit solvent model.
XMIN method is used with max cycles of 1000. Minimization will be stopped if the root-mean-square
of the Cartesian elements of the gradients is less than 0.01 kcal/mol.

- The ddG values were calculated using by MM-GBSA method with MMPBSA.py program.

All minimization and energy evaluations were performed with the development version of [AmberTools16](
http://ambermd.org/AmberTools16-get.html)
