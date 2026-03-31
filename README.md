<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/73d2e0a5-16f1-47d4-a020-dbebd119716c" /><img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/0ff22b0e-8fbf-43cf-891d-0c94c91e7b5c" /># RTOS-Based Touch Sense Control System (STM32 + FreeRTOS)

##  Project Overview

This project implements a real-time touch-based control system using an STM32 microcontroller integrated with FreeRTOS. The system is designed to respond to user touch inputs (or push buttons) through external interrupts and dynamically switch between multiple operating modes.

Each operating mode activates a dedicated task responsible for controlling LED behavior with different timing characteristics. The system also includes a UART-based interface for real-time monitoring and control, making it interactive and flexible.

This project highlights core RTOS concepts such as multitasking, synchronization, interrupt handling, and event-driven execution.


##  Key Features

* Interrupt-based touch input detection using GPIO
* Real-time task scheduling using FreeRTOS
* Dynamic mode switching using Event Groups
* Periodic operations using software timers
* UART interface for command-based control
* Mutex-based protection for shared resources
* Task monitoring using RTOS diagnostic APIs
* High-priority emergency handling mechanism


##  Hardware Requirements

* STM32 Development Board (STM32F4 Series recommended)
* 4 Push Buttons or Capacitive Touch Inputs
* LEDs connected to GPIO pins
* UART interface (115200 baud rate)
* USB-to-Serial converter

##  System Operating Modes
Emergency Mode → High priority LED control 
* Task1  → LED toggle (500 ms)
* Task2 → LED toggle (1000 ms)
* Task3 → LED toggle (1500 ms)

Only one task runs at a time.

###  Emergency Mode

* Triggered via GPIO pin (PA0)
* Activates a high-priority task
* Continuously toggles an emergency LED
* Overrides all other tasks


###  Task 1 Mode

* Triggered via PA1
* Toggles LED at 500 ms interval


###  Task 2 Mode

* Triggered via PA2
* Toggles LED at 1000 ms interval


###  Task 3 Mode

* Triggered via PA3
* Toggles LED at 1500 ms interval



 Note: At any given time, only one task remains active while others are suspended to optimize CPU usage.


##  FreeRTOS Components Used

### Tasks

* Emergency_Task (High Priority)
* Sensor_Task / Task1
* Processing_Task / Task2
* Indicator_Task / Task3
* Control_Task (Manages switching logic)
* UART_Task (Handles communication)


### Synchronization Mechanisms

* Mutex for LED access
* Mutex for UART communication
* Event Groups for mode control


### Event Group Bit Mapping

* EMERGENCY = 0x01
* MODE_1 = 0x02
* MODE_2 = 0x04
* MODE_3 = 0x08


##  UART Command Interface

###  System Status Check

Command:
STATUS?

Description:
Displays the current state of all tasks using FreeRTOS diagnostic functions.


###  Mode Switching Commands

* SET_MODE=EMERG → Activates Emergency Mode
* SET_MODE=TASK1 → Activates Task 1
* SET_MODE=TASK2 → Activates Task 2
* SET_MODE=TASK3 → Activates Task 3


## System Monitoring

The system periodically reports operational statistics such as:

* Number of mode transitions
* Active task details
* System status logs

This helps in analyzing runtime behavior and debugging.


## Interrupt Handling Workflow

1. Touch input detected on GPIO pin
2. External interrupt is triggered
3. Debounce logic is applied using timer
4. Corresponding event bit is set
5. Control task processes the event
6. Required task is resumed
7. Other tasks are suspended


##  Software Architecture

Touch Input
↓
GPIO Interrupt
↓
Debounce Handling
↓
Event Group Update
↓
Control Task Decision
↓
Task Scheduling (Resume/Suspend)
↓
LED Output Action

##  Output Description

* LEDs toggle based on selected mode using RTOS tasks
* Emergency mode overrides all tasks
* UART displays real-time system status and task information

##  Future Improvements

* Add sensor calibration
* Integrate LCD display
* Add mobile app interface for control


##  Learning Outcomes

This project provides practical exposure to:

* Real-Time Operating System (RTOS) concepts
* Task scheduling and prioritization
* Inter-task communication and synchronization
* Interrupt-driven embedded system design
* UART-based communication interface
* Efficient resource management in embedded systems


##  Author

Pallavi Lakumalla
