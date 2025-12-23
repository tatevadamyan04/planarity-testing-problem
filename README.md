# planarity-testing-problem
import networkx as nx
import matplotlib.pyplot as plt

# Օժանդակ ֆունկցիա. գծել գրաֆը պիտակներով
def draw_graph(G, title=None, pos=None):
    plt.figure(figsize=(6,4))
    if pos is None:
        # Օգտագործվում է զսպանակային դասավորություն (spring layout)
        pos = nx.spring_layout(G, seed=42)
    nx.draw(G, pos, with_labels=True, node_size=500)
    if title:
        plt.title(title)
    plt.show()

# Օրինակ 1: K5 (ոչ հարթ)
K5 = nx.complete_graph(5)
is_planar_K5, embedding = nx.check_planarity(K5, False)
print('K5-ը հարթ է՞:', is_planar_K5)
try:
    draw_graph(K5, 'K5 (պետք է լինի ոչ հարթ)')
except Exception:
    pass

# Օրինակ 2: K3,3 (ոչ հարթ)
K33 = nx.complete_bipartite_graph(3,3)
is_planar_K33, emb = nx.check_planarity(K33, False)
print('K3,3-ը հարթ է՞:', is_planar_K33)
try:
    draw_graph(K33, 'K3,3 (պետք է լինի ոչ հարթ)')
except Exception:
    pass

# Օրինակ 3: K4 (հարթ)
K4 = nx.complete_graph(4)
is_planar_K4, emb = nx.check_planarity(K4, False)
print('K4-ը հարթ է՞:', is_planar_K4)

# Եթե հարթ է, ստանալ հարթության ներդրումը և պատկերել այն
if is_planar_K4:
    # Ստանալ շրջանաձև դասավորություն (circular layout)
    pos = nx.circular_layout(K4)
    draw_graph(K4, 'K4 (հարթ)', pos)

# Օրինակ 4: Հարթ ցանց (grid)
G = nx.grid_2d_graph(3,3)
# Փոխակերպել հանգույցների անունները (i,j)-ից ամբողջ թվերի՝ ավելի գեղեցիկ պիտակների համար
G2 = nx.convert_node_labels_to_integers(G, ordering='sorted')
print('Ցանցը հարթ է՞:', nx.check_planarity(G2, False)[0])
draw_graph(G2, '3x3 ցանց (հարթ)')
