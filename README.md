- Generate all pdb files for AMBER with given pdb code (e.g. `1a32`)

    python scripts/pdbgen_from_rosetta.py 1a32
    # Notes: I only include only a single structure in `1a32` for demo

- Generate topology and resart files for AMBER minimization

    python scripts/generate_rst7_parm7_files.py 1a32

- Run minimization
    
    cd 1a32/
    python ../scripts/run_min.py -p empty_tag_11229_0001.parm7 -c "NoH*.rst7" -i ../input/min.in

    # minimized coordinate filename: min*rst7

- Get AMBER potential energy
   
    # Kristin: fill here please

Methods
-------
- Minimization were performed using 14SBonlsc force field and GBNeck2 implicit solvent model.
XMIN method is used with max cycles of 1000. Minimization will be stopped if the root-mean-square
of the Cartesian elements of the gradients is less than 0.01 kcal/mol.

- The potential energies of final snapshots were then evaluated by `sander` program via its Python interface (`pysander`)

All minimization and energy evaluations were performed with the development version of AmberTools16.
