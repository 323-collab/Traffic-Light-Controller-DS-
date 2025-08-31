import matplotlib.pyplot as plt
import matplotlib.patches as patches
import time
from IPython.display import clear_output, display

def draw_junction(active, sec_left):
    fig, ax = plt.subplots(figsize=(6,6))
    ax.set_xlim(0,10)
    ax.set_ylim(0,10)
    ax.set_aspect('equal')
    ax.axis('off')
    
    # Draw roads (cross)
    ax.add_patch(patches.Rectangle((4,0),2,10,facecolor="gray"))
    ax.add_patch(patches.Rectangle((0,4),10,2,facecolor="gray"))
    
    # Traffic lights positions
    positions = [(5,9), (9,5), (5,1), (1,5)]  
    labels = ["Road 1 (North)", "Road 2 (East)", "Road 3 (South)", "Road 4 (West)"]
    
    # Draw lights
    for i, (x,y) in enumerate(positions):
        color = "green" if i == active else "red"
        circle = patches.Circle((x,y),0.5,facecolor=color,edgecolor="black")
        ax.add_patch(circle)
        ax.text(x, y+0.8, labels[i], ha="center", fontsize=10, weight="bold")
    
    # Timer text
    ax.text(5, 0.2, f"⏳ {sec_left} sec left for {labels[active]}", ha="center", fontsize=12, color="blue")
    
    display(fig)
    plt.close()

def traffic_controller():
    active = 0
    while True:
        for sec in range(30, 0, -1):  # 30 sec timer
            clear_output(wait=True)
            draw_junction(active, sec)
            time.sleep(1)
        active = (active + 1) % 4

traffic_controller()
