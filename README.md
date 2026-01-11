Soft and Large‑Area Robot Skin for Tactile Sensing

This repository contains the code developed for my Bachelor end project on soft, large‑area robotic skin for tactile sensing. All theoretical background, methodology, and results are described in detail in the final report.

Several components rely on Linux‑specific packages (such as dolfinx, mpi4py, and ufl), so some notebooks can only be executed in a Linux environment. The sections below describe each file and its requirements.
Project Structure:
1. Indenter_control_sensor_reading.ipynb

Purpose

    Indenter operation and control

    Real‑time sensor data acquisition from both the robotic skin and the indenter’s force sensor

    Sensor data streaming to Live_prediction_plotting.ipynb using network sockets

Notes

    Works together with Live_prediction_plotting.ipynb.

    If the prediction model is retrained on Windows, both notebooks can be merged to avoid socket communication.

2. Live_prediction_plotting.ipynb

Purpose

    Receives real‑time sensor data from the indenter control notebook

    Performs surface pressure estimation using a trained MLP interpolation model

    Generates full stress‑field predictions and performs post‑processing/visualization

Requirements

    Linux only, because Interpolation_model.pkl was encoded on Linux and cannot be loaded on Windows.

3. Simulation_data_generation.ipynb

Purpose

    Generates FEM simulation data for a wide range of indentation scenarios

    Uses dolfinx, mpi4py, and ufl to compute deformation and stress fields

    Exports results to CSV for later model training

Requirements

    Linux only, due to dependencies on dolfinx and MPI‑based packages.

4. Interpolation_training.ipynb

Purpose

    Trains the MLP interpolation model used for real‑time stress estimation

    Outputs the model file Interpolation_model.pkl

Notes

    Can be run on Windows or Linux.

    Training the model on Windows allows Live_prediction_plotting.ipynb to run on Windows as well, enabling a combined real‑time workflow without sockets.

Summary

    Real‑time sensing and prediction rely on two notebooks communicating via sockets.

    FEM simulation and Linux‑encoded models require a Linux environment.

    Training the model on Windows would remove a lot of complexity in the codes.
