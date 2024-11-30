# California-Water-and-Population-Data-Visualization
This project visualizes California's water area and city population distribution using scatter plots. Bubble sizes represent water/city areas, and color gradients show population. Technologies used: Python, Matplotlib, Pandas, Seaborn. It demonstrates data manipulation and advanced geographic data visualization skills.

lat2, lon2 = df['latd'], df['longd']
population, area = df['population_total'], df['area_total_km2']

sns.set_theme()
plt.style.use('ggplot')
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(20,8))

# Scatter plot for cities' population and area
img1 = ax1.scatter(lon2, lat2, s=area, c=np.log10(population), linewidths=0, alpha=0.5, cmap='viridis')
ax1.set(title="California Cities: Population and Distribution",
        xlabel="Latitude",
        ylabel="Longitude")
ax1.axis('equal')

# Adding legend for city area in the first subplot (ax1)
area_range = [50, 100, 300, 500]
for area in area_range:
    ax1.scatter([], [], c='k', s=area, alpha=0.4, label=str(area) + ' km$^2$')
ax1.legend(labelspacing=1, title='City Area')

# Colorbar for population in the first subplot
fig.colorbar(img1, ax=ax1, label='log$_{10}$(Population)')
img1.set_clim(3, 7)

# Scatter plot for water area and frequency in the second subplot (ax2)
water_area, water_f = df['area_water_km2'], df['water_frequency']
img2 = ax2.scatter(lon2, lat2, s=water_area*10, c=np.log10(water_f), cmap='inferno', alpha=0.6)
ax2.set(title="California Cities: Water Area and Frequency",
        xlabel="Latitude",
        ylabel="Longitude")

# Adding legend for water area in the second subplot (ax2)
waterarea_range = [30, 60, 90, 120]
for water_area in waterarea_range:
    ax2.scatter([], [], s=water_area*10, label=str(water_area) + ' km$^2$')
ax2.legend(labelspacing=2, title="Water Area")

# Colorbar for water frequency in the second subplot
fig.colorbar(img2, ax=ax2, label='log$_{10}$(Water Frequency)')

# Show the final combined plot
plt.tight_layout()  # Adjust layout to prevent overlapping
plt.savefig('CaliforniaInformation.png', bbox_inches='tight')

plt.show()


![CaliforniaInformation](https://github.com/user-attachments/assets/8af3621c-0eaf-47d7-bada-4f5d4f3513d3)
