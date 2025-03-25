This repository contains simulation scripts and data for the folowing preprint:

**Daniel Tan, Dilimulati Aierken, and Jerelle A. Joseph. "Interaction networks within biomolecular condensates feature topological cliques near the interface". bioRxiv (2025)**

## Simulation Description

Here we provide both simulation codes for FUS-LCD and HP sequence simulations in the folder [./sims/](./sims).
* Folder [./sims/216x_FUS-LCD_T=270K/](./sims/216x_FUS-LCD_T=270K/) contains production run simulation input scripts for simulating 216 FUS-LCD chains at $T = 270\mathrm{ K}$ using [LAMMPS](https://www.lammps.org/) (version 23 Jun 2022) with the [Mpipi](https://www.nature.com/articles/s43588-021-00155-3) forcefield. An example output trajectory file from the end of the simulation is also included.
  
* Folder [./sims/125x_HP_fh=0.14_T=0.5/](./sims/125x_HP_fh=0.14_T=0.5/) contains production run simulation input scripts for simulating 125 copies of an HP model sequence (hydrophobic fraction $f_{\mathrm{h}} = 0.14$) at $T^* = 0.5\text{ }k_{\mathrm{B}}T/\epsilon$ using [LAMMPS](https://www.lammps.org/) (version 23 Jun 2022). An example output trajectory file from the end of the simulation is also included.

## Data Description

Data is organized based on visualized figures in the manuscript and is placed in the folder [./data/](./data/).
  * Folder [./data/Figure1/](./data/Figure1/) contains small-world coefficients and graph edge densities of 50 sampled frames from each simulation.
  * Folder [./data/Figure2/](./data/Figure2/) contains spatial and temporal distribution data for network hubs and cliques.
  * Folder [./data/Figure3/](./data/Figure3/) contains power-law correlation data for chain conformations and node betweenness centrality.
    * For visualizing the adjacency matrix [Fig3a_FUS_frame_graph_adjacency_matrix.npy](./data/Figure3/Fig3a_FUS_frame_graph_adjacency_matrix.npy), the following code can be used
      ```py
      import networkx as nx
      import matplotlib.pyplot as plt
      import numpy as np
      ixnmat = np.load('Fig3a_FUS_frame_graph_adjacency_matrix.npy', allow_pickle=True).item()
      key = list(ixnmat.keys())[32]
      G = nx.Graph()
      NMOL=216
      for j in range(NMOL):
          G.add_node(j + 1)
      for j in range(len(ixnmat[key])):
          for k in range(j):
              if ixnmat[key][j][k] > 0: G.add_edge(j+1,k+1)
      cbs = nx.betweenness_centrality(G, normalized=True)
      pos = nx.kamada_kawai_layout(G, scale = 0.75)
      fig, ax = plt.subplots()

      nx.draw_networkx_edges(G, pos, ax=ax)
      nx.draw_networkx_nodes(G, pos, ax=ax)
      ```
  * Folder [./data/Figure4/](./data/Figure4/) contains power-law correlation data for chain displacements and node betweenness centrality.
    
