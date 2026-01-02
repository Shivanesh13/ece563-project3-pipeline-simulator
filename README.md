# ECE 563 Project 3.1: Pipeline Simulator

## Overview
This project implements a detailed out-of-order pipeline simulator that models modern processor pipelines with instruction scheduling, register renaming, and reorder buffers. The simulator analyzes pipeline performance and demonstrates advanced computer architecture concepts.

## Features
- **Out-of-Order Execution**: Advanced pipeline with instruction reordering
- **Register Renaming**: Eliminates false dependencies (WAR/WAW hazards)
- **Reorder Buffer (ROB)**: Manages instruction completion and retirement
- **Reservation Stations**: Handles instruction dispatch and execution
- **Branch Prediction**: Integrated branch prediction for control flow
- **Performance Analysis**: Detailed pipeline statistics and bottleneck analysis

## Project Structure
```
Project_3_1/
├── cpp_files/            # Main implementation
│   ├── Makefile
│   ├── sim_proc.cc/h     # Pipeline simulator
│   ├── sim               # Compiled executable
│   ├── test_*.txt        # Test case outputs
│   ├── val_*.txt         # Validation traces
│   └── README            # Basic build instructions
├── proj3-traces/         # Benchmark trace files
│   ├── val_trace_gcc1
│   └── val_trace_perl1
├── validation/           # Expected outputs for validation
│   ├── val1.txt - val8.txt
└── *.zip                 # Project archives
```

## Pipeline Architecture

### Key Components
- **Instruction Fetch**: Fetches instructions from trace
- **Decode/Rename**: Decodes instructions and performs register renaming
- **Dispatch**: Sends instructions to reservation stations
- **Issue/Execute**: Out-of-order execution when operands are ready
- **Writeback**: Writes results back to registers/reorder buffer
- **Commit**: Retires completed instructions in order

### Advanced Features
- **Speculative Execution**: Executes beyond branches using prediction
- **Memory Disambiguation**: Handles load/store dependencies
- **Multiple Functional Units**: Separate units for different instruction types

## Build Instructions
```bash
cd cpp_files
make clean
make
```

## Usage

### Command Line Format
```bash
./sim <ROB_SIZE> <IQ_SIZE> <WIDTH> <trace_file>
```

### Parameters
- `ROB_SIZE`: Reorder buffer size (number of entries)
- `IQ_SIZE`: Issue queue size (number of entries)
- `WIDTH`: Pipeline width (instructions per cycle for fetch/dispatch/commit)
- `trace_file`: Path to instruction trace file

### Example Usage
```bash
# Standard configuration: 128 ROB, 32 IQ, width 4
./sim 128 32 4 gcc_trace.txt

# Conservative configuration: 64 ROB, 16 IQ, width 2
./sim 64 16 2 gcc_trace.txt

# Aggressive configuration: 256 ROB, 64 IQ, width 8
./sim 256 64 8 gcc_trace.txt

# View output with less
./sim 128 32 4 gcc_trace.txt | less
```

## Trace Files
- `gcc_trace.txt`: GCC compilation instruction traces
- `val_trace_gcc1`: GCC validation trace
- `val_trace_perl1`: Perl validation trace

## Performance Metrics

The simulator provides comprehensive pipeline statistics:
- **IPC (Instructions Per Cycle)**: Overall pipeline throughput
- **Branch Misprediction Rate**: Control flow prediction accuracy
- **Pipeline Stalls**: Breakdown of stall causes
- **Resource Utilization**: Usage statistics for functional units
- **Instruction Mix Analysis**: Breakdown by instruction types

## Key Results and Analysis

### Pipeline Width Impact
Analysis shows how pipeline width affects overall performance:
- Diminishing returns with increased width
- Memory-bound applications benefit less from wider pipelines
- Branch mispredictions limit maximum IPC

### ROB and IQ Sizing
The project evaluates different buffer sizes:
- Larger ROBs help with long-latency operations
- Issue queue size affects dispatch efficiency
- Optimal sizes depend on application characteristics

### Validation
The `validation/` directory contains expected outputs (`val1.txt` through `val8.txt`) for different simulator configurations. These are used to verify simulator correctness.

## Test Cases
The project includes multiple test cases (`test_1.txt` through `test_8.txt`) that validate different aspects of pipeline operation:
- Basic instruction execution
- Hazard handling
- Branch prediction
- Memory operations
- Complex instruction sequences

## Dependencies
- C++ compiler (g++ recommended)
- Make build system

## Output Format
The simulator outputs detailed statistics including:
- Pipeline configuration summary
- Execution statistics (cycles, instructions, IPC)
- Branch prediction performance
- Pipeline stall analysis
- Resource utilization metrics

## Academic Context
This project is part of ECE 563: Computer Architecture, demonstrating advanced pipeline concepts used in modern out-of-order processors. The simulator illustrates:
- Instruction-level parallelism exploitation
- Register renaming techniques
- Out-of-order execution principles
- Pipeline hazard management
- Performance bottlenecks in real workloads

## Learning Objectives
This implementation demonstrates:
1. **Pipeline Design**: Balancing complexity and performance
2. **Resource Management**: Efficient allocation of pipeline resources
3. **Dependency Analysis**: Managing instruction dependencies in hardware
4. **Performance Modeling**: Understanding factors limiting processor performance
