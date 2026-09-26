# ECG FPGA HLS Dashboard

## Project Overview

This project implements an **ECG classification dashboard integrated with FPGA acceleration on the PYNQ-Z2 board**.

The system includes two main components:

- A **Windows-based ECG dashboard**
- An **HLS-based inference server running on the PYNQ-Z2**

The FPGA accelerator is developed using **High-Level Synthesis (HLS)** and deployed to the PYNQ-Z2 using the generated `.bit` and `.hwh` files.

## System Architecture

The Windows computer runs the ECG dashboard using **FastAPI**. The dashboard allows the user to load ECG data, select an inference backend, check the FPGA connection, and run ECG predictions.

The PYNQ-Z2 runs a Python API server that loads the FPGA overlay and provides ECG inference services through a REST API.

The Windows computer and the PYNQ-Z2 communicate through an Ethernet connection using HTTP requests.

## FPGA HLS Inference

For FPGA inference, the dashboard provides the following backend:

```text
FPGA HLS Q4.12
```

When the user starts a prediction, the dashboard sends ECG beat samples to the PYNQ-Z2 through the REST API.

The Python server on the PYNQ-Z2 receives the input data and transfers it to the HLS accelerator implemented on the FPGA.

The FPGA accelerator processes the ECG samples using **Q4.12 fixed-point arithmetic** and produces the classification result.

The result is then returned to the Windows dashboard and displayed to the user.

## System Workflow

The system operates in the following sequence:

1. ECG data is loaded into the Windows dashboard.
2. The user selects an inference backend.
3. The dashboard sends the selected ECG beat to the PYNQ-Z2.
4. The PYNQ-Z2 API server receives the ECG samples.
5. The FPGA HLS accelerator performs the inference.
6. The classification result is returned to the API server.
7. The API server sends the result back to the Windows dashboard.
8. The dashboard displays the prediction result.

## Communication

The Windows computer and the PYNQ-Z2 are connected through Ethernet.

The dashboard communicates with the PYNQ-Z2 using a REST API. The PYNQ-Z2 acts as the hardware inference server, while the Windows computer is responsible for the user interface, data handling, and result visualization.

## Main Features

- ECG beat classification
- FPGA-accelerated inference
- Remote inference through REST API
- FPGA connection checking
- Multiple inference backend support
- Multi-backend prediction comparison
- Windows-based ECG dashboard
- PYNQ-Z2 hardware acceleration

## Technologies Used

- Python
- FastAPI
- Uvicorn
- PYNQ-Z2
- FPGA
- High-Level Synthesis (HLS)
- REST API
- Ethernet
- Q4.12 fixed-point arithmetic

## Summary

This project integrates a **Windows-based ECG dashboard** with an **HLS-based FPGA accelerator running on the PYNQ-Z2**.

The Windows dashboard handles ECG data, user interaction, and result visualization, while the PYNQ-Z2 performs hardware-accelerated ECG inference.

Communication between the two systems is implemented using a REST API over Ethernet.
