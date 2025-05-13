# Philosophers

**"I never thought philosophy would be so deadly"**

This repository contains my implementation of the **Philosophers** project developed as part of the 42 School curriculum. This project explores the fundamentals of concurrent programming using threads, mutexes, processes, and semaphores — through a simulation of the classical *Dining Philosophers Problem*.

> **Disclaimer:** This project is for educational and demonstrative purposes only.

## Table of Contents

- [Overview](#overview)
- [Objectives](#objectives)
- [Common Instructions](#common-instructions)
- [Mandatory Part](#mandatory-part)
- [Bonus Part](#bonus-part)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Logging Format](#logging-format)
- [Error Handling](#error-handling)
- [Acknowledgments](#acknowledgments)
- [Disclaimer](#disclaimer)
- [License](#license)

## Overview

In this project, a number of philosophers sit around a table and alternate between eating, sleeping, and thinking. Each needs two forks to eat, and there is only one fork between each pair of philosophers. The simulation must manage resource sharing and avoid starvation or deadlocks using multithreading (or multiprocessing in the bonus).

## Objectives

- Understand and implement **threading**, **mutexes**, and **semaphores**
- Learn about **race conditions**, **deadlocks**, and **synchronization**
- Implement **safe concurrent programming** in C
- Avoid **global variables**
- Use **POSIX threads** and **processes** effectively

## Common Instructions

- Written in **C**, following the strict 42 Norm
- No memory leaks or data races allowed
- Global variables are **forbidden**
- A Makefile must be provided with the rules: `NAME`, `all`, `clean`, `fclean`, `re`
- Only the following functions are allowed:
  - `memset`, `printf`, `malloc`, `free`, `write`, `usleep`, `gettimeofday`
  - `pthread_create`, `pthread_detach`, `pthread_join`
  - `pthread_mutex_*` (mandatory)
  - `fork`, `kill`, `exit`, `waitpid`, `sem_*` (bonus)

## Mandatory Part

### Program: `philo`

- One thread per philosopher
- One mutex per fork
- The simulation must accept the following arguments:

```sh
./philo number_of_philosophers time_to_die time_to_eat time_to_sleep [number_of_times_each_philosopher_must_eat]
```

**Arguments:**
- `number_of_philosophers`: Number of philosophers and forks
- `time_to_die`: Time in ms a philosopher can go without eating before dying
- `time_to_eat`: Time in ms a philosopher takes to eat (while holding 2 forks)
- `time_to_sleep`: Time in ms a philosopher spends sleeping
- `number_of_times_each_philosopher_must_eat` (optional): Ends simulation if all philosophers eat at least this many times

**Rules:**
- Philosophers must pick up both forks to eat
- If a philosopher doesn't eat within `time_to_die` ms, they die
- Simulation ends if a philosopher dies or if the optional meal count is reached for all
- Output must be thread-safe and timestamped in ms

## Bonus Part

### Program: `philo_bonus`

- Uses processes instead of threads
- Forks are represented by a semaphore instead of individual mutexes
- The behavior and arguments are the same as in the mandatory part

**Additional Rules:**
- Each philosopher is a separate process
- Forks are stored centrally and accessed via a semaphore
- The main process supervises the simulation but does not act as a philosopher

## Project Structure

```
philosophers/
├── philo/            # Mandatory part (threads and mutexes)
│   ├── *.c, *.h
│   └── Makefile
├── philo_bonus/      # Bonus part (processes and semaphores)
│   ├── *.c, *.h
│   └── Makefile
├── README.md
```

## Installation

1. **Clone the Repository:**

   ```sh
   git clone https://github.com/marco-ht/Philosophers.git
   ```

2. **Build the Project:**

   Use the provided Makefile to compile your source files:

   ```sh
   cd philosophers/philo
   make
   ```

   This command will produce the executable named `philo`.

   For the bonus version:

   ```sh
   cd ../philo_bonus
   make
   ```

## Usage

**Mandatory Example:**

```sh
./philo 5 800 200 200
```
Start simulation with 5 philosophers, 800 ms time to die, 200 ms to eat, 200 ms to sleep.

```sh
./philo 5 800 200 200 7
```
Each philosopher must eat at least 7 times; simulation ends when done.

## Logging Format

Each action by a philosopher must be printed in the following format:

```
[timestamp_in_ms] X has taken a fork
[timestamp_in_ms] X is eating
[timestamp_in_ms] X is sleeping
[timestamp_in_ms] X is thinking
[timestamp_in_ms] X died
```

- Replace X with the philosopher number
- Ensure messages are not interleaved between threads
- Death message must be printed within 10ms of actual death

## Error Handling

- All incorrect input or allocation failures must return a clean error
- Simulation must not crash under any conditions
- Threads or processes must be joined or terminated cleanly

## Acknowledgments

- Thanks to the 42 community, mentors, and fellow students for their guidance and support.
- Inspired by the classic Dining Philosophers Problem by Edsger Dijkstra.

## Disclaimer

**IMPORTANT**:
This project was developed solely as part of the educational curriculum at 42 School. The code in this repository is published only for demonstration purposes to showcase my programming and system-level development skills.

**Academic Integrity Notice**:
It is strictly prohibited to copy or present this code as your own work in any academic submissions at 42 School. Any misuse or uncredited use of this project will be considered a violation of 42 School's academic policies.

## License

This repository is licensed under the Creative Commons - NonCommercial-NoDerivatives (CC BY-NC-ND 4.0) license. You are free to share this repository as long as you:

- Provide appropriate credit.
- Do not use it for commercial purposes.
- Do not modify, transform, or build upon the material.

For further details, please refer to the CC BY-NC-ND 4.0 license documentation.

Developed with dedication and in strict adherence to the high standards of 42 School.
