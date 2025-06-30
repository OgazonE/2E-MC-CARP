# Two-Echelon Multi-Commodity Waste Collection (2E-MC-CARP) Dataset

This repository contains input files for the **Two-Echelon Multi-Commodity Capacitated Arc Routing Problem (2E-MC-CARP)**, extending the benchmark dataset introduced by Kiilerich and Wøhlk (2018). The extensions include information on intermediate dumping sites and treatment plants, enabling the study of realistic two-echelon waste collection systems with multiple waste streams.

## Repository Structure

Each instance includes:

- LN_Data/`graph.dat`: Graph file with first echelon road network, demand edges, and waste stream data.
- LN_Data/`WGS84.csv`: Linking nodes geolocation data.
- Vehicle_Data/`.veh`: Vehicle file specifying available collection vehicles and compression factors.
- DS_Data/`DS_n.csv`: Dumping sites geolocation data for n sites.
- PP_Data/`PP_n.csv`: Processing plants geolocation data for n plants. 
 
---

## 1. Graph Files



