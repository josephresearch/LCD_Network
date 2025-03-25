This repository contains the data used in the folowing preprint:

**Daniel Tan, Dilimulati Aierken, and Jerelle A. Joseph. "Biomolecular condensate networks feature topological cliques near the interface". bioRxiv (2025): 2025-03.**


## Data Description
Data is organized based on visualized figures in the manuscrip and placed in the folder [./data/](./data/).
  * Folder [./data/Figure1/](./data/Figure1/) contains small-world coeffecients and graph network densities of 50 sampled frames.
  * Folder [./data/Figure2/](./data/Figure2/) contains spatial and temporal distribution network hubs and cliques.
  * Folder [./data/Figure3/](./data/Figure3/) contains power-law correlation data for chain conformations and node betwenness centrality.
    * For visulizing the adjacency matrix [Fig3a_FUS_frame_graph_adjacency_matrix.npy](./data/Figure3/Fig3a_FUS_frame_graph_adjacency_matrix.npy), the following code can be used
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
  * Folder [./data/Figure4/](./data/Figure4/) contains power-law correlation data for chain displacements and node betwenness centrality.
    
