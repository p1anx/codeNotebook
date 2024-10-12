# code0
```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

# Define the file path where the CSV files are located
filePath = "F:\\BaiduSyncdisk\\2_科研\\机械天线\\1-MA\\仿真\\comsol\\1_comsol_summary\\for_paper\\2-multiple_magnet_3d\\matlab\\Hx\\"
# List of CSV file names to be read and plotted
fileName = ["2mag_Hx.csv", "3mag_Hx.csv", "4mag_Hx.csv", "5mag_Hx.csv"]

# Create a 2x2 grid of subplots with a specified figure size
fig, axs = plt.subplots(2, 2, figsize=(10, 8))

# Iterate over each file name and index
for i, name in enumerate(fileName):
    # Construct the full file path
    file = filePath + name
    # Read the CSV file into a DataFrame
    data = pd.read_csv(file)
    # Generate a time array for the x-axis
    t = np.linspace(0, 1, len(data))
    
    # Select the appropriate subplot
    ax = axs[i // 2, i % 2]
    # Plot the data on the current subplot
    ax.plot(t, data)
    # Set the title of the subplot to the file name
    ax.set_title(name)
    # Enable grid for the subplot
    ax.grid(True)

# Adjust layout to prevent overlap between subplots
plt.tight_layout()
# Display the plot
plt.show()
```

# code1










