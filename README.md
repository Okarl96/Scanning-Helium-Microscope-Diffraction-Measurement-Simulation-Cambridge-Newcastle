# Scanning-Helium-Microscope-Diffraction-Measuement-Simulation-Newcastle

Created by **Ke Wang**.

It is an interactive script that simulates the diffraction measurement of the SHeM at the University of Newcastle. It allows different surface lattice structures and different detector geometry to be simulated. The input of the Multiscat is also implemented, which makes it a good script to visualize the multiscat result.

<img width="205" alt="parameters" src="https://github.com/user-attachments/assets/6128c8f0-106a-4412-a18d-2b52705e9528">

**Diffraction channel**: Number of diffraction channels in the script. (10 means the diffraction channels from [-10,-10] [-10,-9]... to ...[9,10] [10,10] will be examined)

**Lattice constant**: The real space lattice separation.

**Lattice vector**: Lattice vector of the unit cell.

**Beam Energy**: The simulation assumes the Helium beam is monochromatic.

**In-plane & Out-plane axis**: The full length of two axes of the elliptical detector aperture.

![schematic figure](https://github.com/user-attachments/assets/94210741-b96e-479f-b6ef-2e182c50070c)
Figure adopted from https://doi.org/10.1016/j.ultramic.2024.113951

**Detector Angle**: The detection angle $\theta$ of the detector.

**Detector Radius**: The simulation package assumes the angular movement of the detector is circular.

**Detector Height**: The relative height of the detector to the sample in the Y axis, shown in the figure. 

**Incident angle theta**: The incident polar angle of the helium beam.

**Incident angle phi**: The incident azimuthal angle of the helium beam. (currently not working)

**Lattice orientation**: To simulate the rotation of the sample or different crystal orientations in polycrystalline samples.

**reverse_latt_orientation_for_simulation**: The Multiscat changes the incident helium beam azimuthal angle, and the simulation script changes the lattice orientation. One is clockwise and the other anticlockwise, usually a reverse operation is needed if Multiscat is imported.

**Meshgrid resolution**: The number of pixels in the mesh grid script, default=1000.

**Kx, Ky mesh range**: The minimum and maximum of the $\Delta K$ displayed in the figure.

**Peak width**: The standard deviation of the Normal Distribution that gives width to each diffraction peak.

**use_reduce_in_signal_along_z**, **Pattern width**, **Pattern width**, **use_bg_diffuse_signal**, **Diffuse BG width**, **Diffuse BG scale** are functions that generate background noise for the Cambridge SHeM, can be used here to test the code but future work of simulating background noise in the Newcastle SHeM is needed.

**use_multiscat**: Import multiscat datafile and assign diffraction channel intensites accordingly.

**Angle step in Multiscat**: The step of change in incident helium beam azimuthal angle produced by the Multiscat, usually 2.5 or 1 degree.

**Angle compensation**: Sometimes a difference in the lattice vector interpreted from the same unit cell used in the script and Multiscat may need a compensation.

**line_plot**: The simulated line scan, turn off for better performance in generating the K space figure.

**plot_detector_path**: The detection window for a certain $\theta$ and height range of the detector aperture projected to the $K$ space.

**Detector Angle Range and Height Range**: The range of $\Theta$ and height used in the "line_plot" and "plot_detector_path".

**Angle and Height Range linspace**: The resolution of the Angle Range and Height Range, higher for a smooth line, lower for better performance.

**return_line_result**: Show the x and y values in the "line_plot".

**save_plots**: Click to save the plot, but keep it turned off when adjusting parameters.

**save_plots_index**: Name of the picture file saved in "save_plots".





An example of plotting the 2D diffraction measurement is in the notebook.

This is the place where the parameters of importing these Multiscat results correctly into the simulation are recorded.

<img width="846" alt="multiscat data" src="https://github.com/user-attachments/assets/e8950261-0a51-4261-9149-3674a98b6325">

These are the parameters for generating the 2D plot. The function of each parameter is exactly the same as introduced above.

<img width="926" alt="2d example" src="https://github.com/user-attachments/assets/fd185cb1-e5d6-4974-8a33-78c088b244af">

There is one thing to be noticed, if one wants to import Multiscat results, the 'angle_ranges' should be changed according to whether the **reverse_latt_orientation_for_simulation** is enabled or not and the value of **Angle compensation**. For example: if we are using 'MoS2_2H_NEW.mtl', the proper importing parameters are 'angle_compensate = -30, reverse_latt_orientation_for_simulation=True'. The values in the 'latt_orientation', 60, will be summed by the 'angle_compensate' which is -30. The actual lattice orientation imported from the Multiscat will be 30. The 'reverse_latt_orientation_for_simulation' is enabled which means the simulation will generate lattice orientations at -60. In summary, we are assigning Multiscat results (at 30 deg) to simulated diffraction peaks at a lattice orientation (-60 deg).

To generate the simulated 2D plot. The dkx, dky, and intensity array will be reshaped into meshgrid structure.

<img width="278" alt="plot" src="https://github.com/user-attachments/assets/3c1152dd-7968-45db-bf49-53eeddf23c5a">
