# Two-Echelon Multi-Commodity Waste Collection (2E-MC-CARP) Dataset

This repository contains input files for the **Two-Echelon Multi-Commodity Capacitated Arc Routing Problem (2E-MC-CARP)**, extending the MC-CARP benchmark dataset introduced by Kiilerich and Wøhlk (2018). The extensions include information on intermediate dumping sites and treatment plants, enabling the study of realistic two-echelon waste collection systems with multiple waste streams.

## Repository Structure

Each instance includes:

- LN_Data/`graph.dat`: Graph file with first echelon road network, demand edges, and waste stream data.
- LN_Data/`WGS84.csv`: Linking nodes geolocation data.
- Vehicle_Data/`.veh`: Vehicle file specifying available collection vehicles and compression factors.
- DS_Data/`DS_n.csv`: Dumping sites geolocation data for n sites.
- PP_Data/`PP_n.csv`: Treatment plants geolocation data for n plants. 
 
---

## 1. Graph Files (`graph.dat`)

### Header

1. Problem type (e.g., MC-CARP)
2. Number of nodes
3. Number of edges
4. Depot node number


### Fractions Section

Defines the waste streams (fractions) and their collection intervals (fixed to 14 days in this dataset):

NumberOfFractions: 4
NumberOfIntervalsForFraction Glass_Metal_Plastic 1 14
NumberOfIntervalsForFraction General 1 14
NumberOfIntervalsForFraction Organic 1 14
NumberOfIntervalsForFraction Paper 1 14

### Graph Table

Starts with the keyword `GRAPH`, followed by a header like:
EdgeNumber EdgeId StartNodeNumber EndNodeNumber Cost Demand_0 Bins_0 Demand_1 Bins_1 ...


Each `Demand_x` refers to a waste stream in the same order as listed above. Demand is in liters.

### Edge Data 

Delimited by `START` and `END`. Each row corresponds to an edge.

---

## 2. Linking nodes geolocation (`WGS84.csv`)

This file lists all nodes in the LN graph, including both projected and geographic coordinates.
Each row contains:

- NodeNumber: Internal sequential index used for modeling.
- NodeId: Original node identifier from the source graph.
- x / y: Projected coordinates (in meters, WGS84 / UTM zone 32N).
- latitude / longitude: Geographic coordinates in decimal degrees (WGS84).

This file allows for the mapping and geospatial visualization of the LN graph and enables association of facilities (e.g., dumping sites or treatment plants) to network nodes.

---

## 3. Vehicle Files (`.veh`)

Each file defines a (heterogeneous) fleet of collection vehicles.

### Format Example

NumberVehicleTypes:	6

VehicleType:		1  <-Here follows information for the first (and only) type.  
NumberVehicles		75	<- The number of available vehicles.  
NumberCompartments	2 <- Number of compartments.  
CompartmentCapacities	12500	9300  <- Compartment capacity.  
NumberCompression	9  <-Number if lines to read with compression factors.  
General_Organic		5 <- Compression factor for each waste fraction.  
General			5  
Organic			1  
Paper			4  
Plastic			3  
Glass			1  
Metal			3  
Cardboard		4  
Glass_Metal_Plastic	2  
TravelSpeed		1000 <- The remaining info is not relevant for the 2E-MC-CARP.  
TimeEmptyPerBin		0  
TimeUnload		0  
TimeDurationLimit	1000  
NumberBinsLimit		1000  

- Multiple vehicle types are allowed.
- Compartments can have different sizes.
- Each waste stream has a defined compression factor.
- Dummy timing values are included for completeness but are not used in basic routing models.

---

This dataset extension adds infrastructure data:

### 4. Dumping Sites (`DS_n.csv`)

This file provides geospatial and graph-based information for each available dumping site.

Each row contains:

- Dumping site: Name of the facility.

- latitude / longitude: Geographical coordinates in decimal degrees (WGS84).

- x / y: Projected coordinates in WGS84 / UTM zone 32N (in meters).

- Closest node: Node ID in the NL graph that is closest to the dumping site.

- Closest distance: Distance (in meters) from the dumping site to the closest node.

- Closest time: Time (in seconds) required to traverse from the dumping site to its closest node.

Note: All travel times and distances from the dumping site to any other node are computed under the assumption that the vehicle must first reach the closest node listed in the file. This allows for integration with routing algorithms on the NL graph without embedding dumping sites as explicit nodes.

---

### 5. Treatment Plants (`PP_n.csv`)

This file lists the locations of treatment plants to which second-echelon vehicles deliver sorted waste streams.

Each row includes:

- Plant: Name of the treatment facility.
- latitude / longitude: Geographic coordinates in decimal degrees (WGS84).
- x / y: Projected coordinates in WGS84 / UTM (in meters).

Note: Each treatment plant is assigned to a single waste stream. Locations are selected to reflect realistic distances from the operating zone, allowing for the modeling of long-haul second-echelon trips.

---

## References

- Kiilerich, L., Wøhlk, S., 2018. New large-scale data instances for CARP and new variations of CARP. Inf. Syst. Oper. Res. 56, 1–32. [http://optimization.dk/index.html]

