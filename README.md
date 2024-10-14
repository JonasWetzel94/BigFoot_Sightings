# Bigfoot Sightings Analysis - Power BI Project

🦶 **Bigfoot Sightings Analysis**: This project focuses on analyzing reported Bigfoot sightings across various regions, time periods, and environmental conditions. Using Power BI, the project provides deep insights into the patterns of sightings, helping uncover potential trends and correlations.

🔍 **Explore interactive visuals, DAX measures, and advanced data transformation techniques** to understand how different variables, such as geography, weather, and time of year, affect Bigfoot sighting reports.

# Background

The **Bigfoot Sightings Analysis** was created to explore trends in the data collected from reported sightings of Bigfoot. The project’s aim is to identify geographical hotspots, understand seasonal trends, and analyze environmental conditions that might correlate with sighting patterns. The Power BI dashboard presents this information in an easy-to-understand format for researchers or enthusiasts seeking to draw insights from the data.

### Key Questions Addressed:
1. **Where are the most frequent Bigfoot sightings located?**
2. **What time of year sees the most sightings?**
3. **Are there any environmental or geographical factors that correlate with sighting reports?**
4. **How have the number of sightings changed over the years?**
5. **Is there a regional pattern of Bigfoot sightings?**

# Tools and Techniques I Used

For this analysis, I used the following tools and techniques:
- **Power BI**: The primary tool used to create interactive visuals and perform data exploration.
- **Advanced DAX (Data Analysis Expressions)**: Implemented to calculate trends, aggregations, and seasonal breakdowns of sightings.
- **Data Cleaning and Transformation**: Power Query was used to clean, merge, and reshape the sightings dataset.
- **Conditional Formatting**: Applied to key metrics to highlight regions or periods with high concentrations of sightings.
- **Advanced Power BI Features**: Used custom tooltips, drillthrough capabilities, and bookmarks to enhance user interactivity.

# The Dashboard

### Key Visuals and Insights:

1. **Sightings Over Time**:
   - The **line chart** presents the number of Bigfoot sightings over time, allowing users to visualize any patterns or trends in the frequency of reports. Peaks in sightings during specific periods may point to external factors influencing the data.
   
2. **Geographical Distribution**:
   - The **map visual** pinpoints sighting locations, highlighting **hotspots** where Bigfoot sightings are more frequent. Users can drill down into specific regions to examine data at a more granular level.

3. **Monthly and Seasonal Patterns**:
   - This **bar chart** displays sightings by month, revealing any seasonal trends in reports. A peak in sightings during the summer months, for example, may correlate with factors like increased outdoor activity or certain weather patterns.

4. **Top Regions for Sightings**:
   - The **heatmap** visual categorizes the data by state or region, highlighting areas with the highest number of sightings. The regions are color-coded, with darker shades representing higher concentrations of reports.
   
5. **Environmental Conditions**:
   - Analyzing environmental variables, such as **weather patterns** or **moon phases**, this visual explores whether there’s a correlation between certain conditions and an increase in sightings. For example, a spike in reports during foggy or moonlit nights may suggest environmental influences.

# The Analysis

### 1. Geographic Hotspots for Sightings

The map visual helps users quickly identify the regions with the most sightings. By plotting the sightings on a map, I was able to highlight areas such as the **Pacific Northwest** where reports are particularly concentrated. Users can filter by state or zoom in to explore local hotspots.

**Advanced DAX for Region-based Analysis**:
```dax
Sightings Count by Region = 
CALCULATE(
    COUNT('Sightings'[SightingID]),
    'Sightings'[Region] = "Pacific Northwest"
)
```

This DAX formula calculates the number of sightings in a specific region, allowing for region-based analysis.

### 2. Temporal Analysis of Sightings

The **line chart** and **bar chart** visuals were used to explore the time dimension of sightings, tracking both monthly and yearly trends. 

**DAX for Year-over-Year Sightings Growth**:
```dax
YoY Sightings Growth = 
DIVIDE(
    [Total Sightings] - CALCULATE([Total Sightings], PREVIOUSYEAR('Date'[Year])),
    CALCULATE([Total Sightings], PREVIOUSYEAR('Date'[Year]))
)
```

This DAX measure tracks the **year-over-year growth** of Bigfoot sightings, helping to identify if sightings are increasing or decreasing over time.

### 3. Seasonal Trends

By analyzing sightings data on a **monthly and seasonal basis**, we can determine when sightings are most frequent. This insight is helpful for those interested in understanding the external factors influencing reports, such as weather or regional tourism.

**DAX for Sightings by Month**:
```dax
Sightings by Month = 
CALCULATE(
    COUNT('Sightings'[SightingID]),
    MONTH('Sightings'[Date]) = MONTH(TODAY())
)
```

This formula counts the sightings that occurred in the current month over the years, helping to identify **seasonal trends**.

# Advanced SQL Query for Bigfoot Sightings Analysis

In addition to Power BI’s DAX calculations, I also used SQL to clean and prepare the data for analysis. Here is an advanced SQL query used for aggregating sightings data by geographical and environmental conditions:

```sql
WITH WeatherConditionSummary AS (
    SELECT 
        Region,
        COUNT(SightingID) AS TotalSightings,
        AVG(CASE WHEN Weather = 'Foggy' THEN 1 ELSE 0 END) AS FoggySightingsRatio,
        AVG(CASE WHEN Weather = 'Rainy' THEN 1 ELSE 0 END) AS RainySightingsRatio,
        AVG(CASE WHEN MoonPhase = 'Full Moon' THEN 1 ELSE 0 END) AS FullMoonSightingsRatio
    FROM 
        dbo.BigfootSightings
    GROUP BY 
        Region
)

SELECT 
    Region,
    TotalSightings,
    FoggySightingsRatio,
    RainySightingsRatio,
    FullMoonSightingsRatio
FROM 
    WeatherConditionSummary
ORDER BY 
    TotalSightings DESC;
```

This query calculates the ratio of sightings that occurred under specific weather conditions or moon phases, offering insights into how environmental factors might affect reports.

# Key Insights

1. **Geographical Hotspots**: The analysis revealed clear geographical hotspots, particularly in the **Pacific Northwest**, with some regions reporting significantly higher sightings than others.
   
2. **Seasonal Trends**: The data shows that sightings peak during the **summer months**, suggesting that outdoor activity or tourism may be influencing factors.
   
3. **Environmental Influences**: Conditions like foggy weather or full moon nights appear to correlate with an increase in sighting reports, offering a unique dimension to the analysis.

# What I Learned

🧩 **Advanced DAX for Temporal and Regional Analysis**: Through this project, I honed my DAX skills for analyzing time-based and regional data trends, enabling in-depth insights into when and where Bigfoot sightings occur.

📊 **SQL Data Aggregation**: Using SQL, I aggregated and cleaned the sightings data, providing a solid foundation for analysis in Power BI.

💡 **Patterns in Anomalous Data**: By exploring environmental factors, I developed a deeper understanding of how external conditions can influence data patterns, leading to more nuanced analysis.

# Conclusions

### Key Takeaways:
- **Regionally Focused Patterns**: The Pacific Northwest is the clear leader in Bigfoot sightings, indicating a potential pattern in certain terrains or outdoor activity.
- **Seasonal Variability**: Summer months see the most sightings, likely due to more outdoor activities during warmer weather.
- **Environmental Conditions**: Foggy weather and full moon phases appear to have a slight correlation with higher sighting reports, adding an interesting dimension to the analysis.
