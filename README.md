# ECE297 Final Project - SafeCity

SafeCity is a GIS-based application that visualizes reported incidents and supports incident-aware route exploration in Toronto. The project combines **historical 2023 Toronto Police Service incident data** with **real-time TomTom traffic incidents** and standard map/navigation features.

The historical incident layer is intended as a visualization and route-comparison heuristic. It should not be interpreted as a real-time crime prediction system or as an objective measure of whether a neighborhood is "safe" or "dangerous."

## Source Availability

This project was developed for **ECE297 at the University of Toronto**. The application source code is **not published publicly because of academic-integrity requirements for course work**. This repository therefore contains project documentation, demonstrations, and performance-analysis artifacts rather than the full C++ codebase.

The notebooks included here analyze path-finding and multi-route performance from the completed project. I am happy to discuss the architecture, algorithms, design decisions, testing approach, and my individual contributions in an interview without redistributing restricted course source code.

## Key Features

### 1. Incident Mapping

- Visualizes Points of Interest (POIs) in major cities.
- Displays reported 2023 crime incidents in Toronto sourced from Toronto Police Service data.
- Shows real-time traffic incidents through the TomTom traffic API.
- Opens a sidebar with incident details such as type, date, and neighborhood when users select map elements.

<p align="center">
  <img src="src/POI.png" width="700">
</p>

### 2. User-Friendly Interface

- Visualizes concentrations of reported incidents on the map.
- Adjusts map elements dynamically based on zoom level for improved visibility.

<p align="center">
  <img src="src/SafeCity Demo.gif" width="900">
</p>
<br><br>

### 3. Path Finding with the A* Algorithm

- Performs route planning while considering travel time and street-turn penalties.
- Process:
  1. **Initialize:** Create the graph representation.
  2. **Explore:** Traverse legally connected intersections.
  3. **Evaluate:** Determine whether the destination has been reached and update path costs.
  4. **Return:** Backtrack through the predecessor chain to construct the path.

**Path-finding demo:**

<p align="center">
  <img src="src/path.png" width="700">
</p>
<br>

**Result:**

<p align="center">
  <img src="src/path finding result.png" width="700">
</p>
<br><br>

### 4. Incident-Aware Route Comparison

- Compares candidate routes using the number of historical reported incidents near the route as an additional heuristic.
- This feature is intended for exploration and does not guarantee that a route is safer in real-world conditions.

<p align="center">
  <img src="src/safe path.gif" width="900">
  <br><br><br>
  <img src="src/safe path comparison.png" width="900">
</p>
<br><br>

### 5. Multi-Route Planning

- Allows users to plan routes across multiple destinations.
- Process:
  1. **Create Matrix:** Establish costs between relevant intersections.
  2. **Run Randomized Greedy Search:** Execute 2,000 iterations of the greedy route algorithm.
  3. **Select Route:** Keep the lowest-cost route found across the iterations.
  4. **Identify Depot:** Select the depot with the lowest associated route cost.

**Result:**

<p align="center">
  <img src="src/multi route result.png" width="700">
</p>
<br><br>

## What the Project Demonstrates

- GIS visualization using C++ and map data.
- Integration of historical incident datasets and a real-time traffic API.
- Graph search and route planning with A*.
- Heuristic route comparison using multiple cost signals.
- Interactive map UI design for navigating large spatial datasets.

## Data and Interpretation Limitations

1. **Crime data is historical, not real time.** The crime layer in this project represents reported incidents from 2023. Only the TomTom traffic-incident layer is real time.
2. **Reported incidents are not equivalent to objective neighborhood safety.** Reporting rates, policing patterns, time of day, and many other factors affect the dataset.
3. **Raw incident counts are not population-normalized.** Dense or highly visited areas may naturally contain more reported incidents even if per-capita rates differ.
4. **Incident categories lack full situational context.** A category and map location alone cannot fully describe the circumstances or current risk at a location.
5. **Route heuristics are exploratory.** Minimizing proximity to historical reported incidents does not guarantee a safer trip.

## Future Work

1. Normalize historical incident measures using population or foot-traffic estimates.
2. Add time-of-day and recency weighting to incident visualization.
3. Evaluate route heuristics against better-defined safety metrics rather than raw incident counts.
4. Explore carefully moderated user-submitted incident reports with appropriate verification and privacy protections.
5. Add richer gradient/heat-map visualizations for normalized incident rates.
