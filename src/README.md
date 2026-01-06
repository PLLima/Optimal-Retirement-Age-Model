========================================================================
MINI-PROJECT: DEMOGRAPHIC-ECONOMIC MODELING (PART I)
Group: Sujet7GrB
========================================================================

1. OVERVIEW
-----------
This folder contains the MATLAB Live Scripts (.mlx) for the continuous-state 
simulation of population aging and pension sustainability based on the 
Hock and Weil (2012) model.

2. FILE LIST
------------
The project is modular. Ensure all files are in the same folder:

- run_analysis.mlx       : The MAIN file. Runs the simulation and plots results.
- get_parameters.mlx     : Configuration file containing all model parameters.
- model_dynamics.mlx     : The engine containing the differential equations.
- visualize_results.mlx  : Helper function for generating plots.
- stability_analysis.mlx : Script for calculating eigenvalues and stability.

3. HOW TO RUN THE SIMULATION
----------------------------
Requirement: MATLAB R2016b or later (R2023a+ recommended for Live Scripts).

Step 1: Open MATLAB and navigate to this folder.

Step 2: Double-click 'get_parameters.mlx' to open it.

Step 3: In the "Live Editor" tab at the top, click the "Run All" button.

Step 4: Double-click 'run_analysis.mlx' to open it.

Step 5: In the "Live Editor" tab at the top, click the "Run All" button.
        (The figures will appear directly inside the document).

Step 6: Repeat steps 5 and 6 with the file 'stability_analysis.mlx'.

4. HOW TO CHANGE SCENARIOS
--------------------------
To test different scenarios (e.g., changing fertility preference or 
enabling migration), open 'setup_params.mlx'.

- Change 'theta' to adjust fertility preference.
- Change 'xi' to adjust the cost of child-rearing.
- Set 'P.migration_on = true' to enable migration.
- ...

Save the file and repeat Step 3 to see the new results.