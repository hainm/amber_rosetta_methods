- Run mmgbsa per residue energy decomposition

    ```bash
    # n_proteins = 87
    # Please update decomp_mpi.py to use correct
    # That script will look for a pdblist.txt, a folder having all minimized rst7 files
    # Please update it to your need
    mpirun -n 87 python scripts/decomp_mpi.py

    # To run a single protein
    # ../../../1be908_wt: have min*rst7 and prmtop files
    python ./scripts/decomp_single.py ../../../1be908_wt
    ```

- Get energy for each residue for each structure

    ```bash
    python ./scripts/get_energy_each_snapshot.py 1be908_wt
    ```

- Average energy (from 50 snapshots) for each residue in each protein

   ```bash
   {pdb_folder}/res.csv
   # tot = vdw  + int + eel + pol + sas

   # int: Internal energy contributions
   # vdw: van der Waals energy contributions
   # eel: Electrostatic energy contributions
   # pol: Polar solvation free energy contributions
   # sas: Non-polar solvation free energy contributions

   # tot: Total free energy contributions (sum of previous 5).
   ```
- Get average energy per residue from 50 snapshots
    
   ```bash
   cd 1be908_wt
   python ../scripts/process_residue.py
   # and so on for other proteins
   ```
- See also:

    ```bash
    Section: "Decomposition Data" in http://ambermd.org/doc12/Amber16.pdf (page 675)
    ```

