# Calibration Workflow

This document provides a simplified overview of the calibration workflow implemented in the original industrial prototype.

The purpose of the system was to reduce manual intervention and guide the operator through a controlled, traceable and repeatable calibration process.

## Calibration Modes

The system supports two operating modes.

### Auto Calibration

Auto Calibration is designed to execute the complete calibration sequence autonomously.

After the operator starts the process, the system sequentially processes all standard flow rates from **1 ml/s to 10 ml/s**.

For each flow rate, the system performs the required measurement, calculation and verification stages before automatically moving to the next one.

The main objective of this mode is to minimize operator intervention during the calibration process.

### Manual Calibration

Manual Calibration allows the operator to select only the flow rates required for a specific test.

The operator can choose one or more standard values or enter a custom flow rate when required.

This mode is particularly useful during testing, development and targeted calibration procedures.

The public system demonstration uses Manual Calibration because it allows the complete workflow to be shown without recording the significantly longer full automatic sequence.

---

## Process Overview

The calibration workflow follows these main stages:

1. System initialization
2. Operator authentication
3. Device configuration
4. Calibration mode selection
5. Sensor validation
6. Device setup
7. Injection and data acquisition
8. Calibration calculation
9. Verification
10. Iterative adjustment when required
11. Result validation
12. Data logging and report generation

---

## Operator Authentication

The operator accesses the system using an NFC identification tag.

A manual username and password login is also available as a fallback method.

This authentication step allows the calibration process to remain associated with the operator performing the procedure and improves traceability.

---

## Device Configuration

After authentication, the operator selects the device model and enters the required identification information.

The interface then allows the user to choose between Auto and Manual Calibration.

Once the configuration is complete, the system prepares the hardware and validates the sensor state before beginning the calibration sequence.

---

## Sensor Validation

Before starting an injection, the system checks that the sensors are operating within the expected initial conditions.

If the sensor readings are not suitable, the calibration process is prevented from continuing until the sensor state has been corrected.

This validation is repeated throughout the process to ensure reliable measurements.

---

## Closed-Loop Calibration

The core calibration process operates as an iterative closed-loop workflow.

For each flow rate:

```text
Injection
   ↓
Sensor and device measurements
   ↓
Calibration calculation
   ↓
Updated calibration parameter
   ↓
New injection
   ↓
Verification
   ↓
Valid? ───── Yes ───→ Calibration validated
   │
   No
   ↓
Recalculate and repeat
```

The system compares the measurement results with the expected calibration conditions.

If the result is not valid, the calibration parameter is adjusted and the process is repeated.

To prevent the system from remaining indefinitely in the same calibration step, the number of verification attempts is limited.

If the calibration cannot be validated within the allowed number of attempts, that flow rate is marked as failed and the system continues with the remaining sequence.

---

## Visual Feedback

The calibration interface provides real-time visual feedback for every selected flow rate.

The status grid uses the following color convention:

* **Grey** — the flow rate is currently being processed
* **Green** — calibration has been successfully validated
* **Red** — calibration could not be successfully validated

This allows the operator to understand the overall process status at a glance.

A continuous loading indicator is also displayed while background calibration operations are running.

---

## Safety Control

The calibration interface includes an easily accessible **STOP** control.

This allows the active calibration process to be interrupted immediately when required.

The system was designed so that operational feedback and safety controls remain visible while the calibration sequence is running.

---

## Data Logging and Reporting

Once a calibration step has been successfully validated, its associated data is recorded.

After all selected flow rates have been processed, the system completes the calibration workflow and generates the corresponding result documentation.

The original prototype included automatic data logging and report generation to support traceability and technical evaluation.

---

## Public Documentation Note

This document intentionally describes the calibration workflow at a high level.

Company-specific algorithms, internal communication protocols, calibration parameters, production data and proprietary implementation details are not included in this public repository.
