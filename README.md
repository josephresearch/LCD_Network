This repository contains simulation scripts and data for the folowing preprint:

**Daniel Tan, Dilimulati Aierken, Pablo L. Garcia, and Jerelle A. Joseph. "Biomolecular condensate microstructure is invariant to sequence-encoded molecular and macroscopic properties". Soft Matter (2025)**

## Simulation Description

Here we provide molecular dynamics simulation codes for both FUS-LCD and an example YS binary sequence (S4Yx30) in the folder [./sims/](./sims).
* Folder [./sims/216x-fus-lcd/](./sims/216x-fus-lcd/) contains production run simulation input scripts for simulating 216 FUS-LCD chains at $T = 0.90T_{\rm c}$ and $T = 0.95T_{\rm c}$ using [LAMMPS](https://www.lammps.org/) (version 23 Jun 2022) with the [Mpipi](https://www.nature.com/articles/s43588-021-00155-3) forcefield. An example output trajectory file from the end of the simulation is also included; this trajectory file contains only the final ten frames of simulation due to filesize constraints. 
  
* Folder [./sims/216x-S4Yx30/](./sims/216x-S4Yx30/) contains production run simulation input scripts for simulating 216 copies of an example YS binary sequence (hydrophobic fraction $f_{\mathrm{h}} = 0.20$) at $T = 0.90T_{\rm c}$ and $T = 0.95T_{\rm c}$ using [LAMMPS](https://www.lammps.org/) (version 23 Jun 2022). An example output trajectory file from the end of the simulation is also included; this trajectory file contains only the final ten frames of simulation.

## Data Description

Data is organized based on visualized figures in the manuscript and is placed in the folder [./data/](./data/). Unless otherwise labeled, provided data reflect analyses where condensate interaction networks are constructed by assigning edges between molecules (nodes) A and B if the intermolecular interaction energy $E_{\rm{AB}}<-5k_{\rm B}T$. 
  * Folder [./data/Figure1/](./data/Figure1/) contains data for phase diagrams and surface tension measurements.
  * Folder [./data/Figure2/](./data/Figure2/) contains small-world coefficients, constructed interaction matrices (adjacency matrices of graphs), and intermolecular interaction energies across 50 sampled frames from each simulation.
    * For visualizing adjacency matrices, e.g., [./data/Figure2/LCD/0.90Tc/A1-LCD/ixnmats_5kbT.npy](./data/Figure2/LCD/0.90Tc/A1-LCD/ixnmats_5kbT.npy), the following code can be used
      ```py
      import networkx as nx
      import matplotlib.pyplot as plt
      import numpy as np
      filepath = './data/Figure2/LCD/0.90Tc/A1-LCD/ixnmats_5kbT.npy'
      frame_number = 0 # any of 50 sampled frames, zero-indexed
      ixnmat = np.load(filepath, allow_pickle=True).item()
      key = list(ixnmat.keys())[frame_number]
      G = nx.Graph()
      NMOL = 216
      for j in range(NMOL):
          G.add_node(j + 1)
      for j in range(len(ixnmat[key])):
          for k in range(j):
              if ixnmat[key][j][k] > 0: G.add_edge(j+1,k+1)
      cbs = nx.betweenness_centrality(G, normalized=True) # Compute the betweenness centrality for all nodes in graph
      pos = nx.kamada_kawai_layout(G, scale = 0.75) # Use Kamada-Kawai force-directed layout to organize graph
      fig, ax = plt.subplots()

      nx.draw_networkx_edges(G, pos, ax=ax)
      nx.draw_networkx_nodes(G, pos, ax=ax)
      ```
  * Folder [./data/Figure3/](./data/Figure3/) contains spatial and temporal distribution data for network hubs and cliques.
  * Folder [./data/Figure4/](./data/Figure4/) contains power-law correlation data for chain conformations (radius of gyration $R_{\rm g}$, relative shape anisotropy $\kappa^2$) and node betweenness centrality.
  * Folder [./data/Figure5/](./data/Figure5/) contains power-law correlation data for molecular displacements and node betweenness centrality, as well as data on the relative displacements of the hub and clique mesoscale features. 
    
