# Design Philosophy

## Core Principles

Odometer follows these key design principles:

- **Clear Hierarchy**: Commands follow odometer → verb → noun pattern
- **Explicit Naming**: Self-explanatory verbs like measure, list, show, and nouns like gas-limit, clients
- **Required Arguments First**: Essential parameters come first
- **Sensible Defaults**: Reasonable defaults for duration, tps, concurrency
- **Output Flexibility**: Multiple output formats for different needs
- **Extensibility**: Easy addition of new benchmark types
- **Discoverability**: Consistent help system

> [!NOTE]
> This document outlines the design philosophy and command structure for Odometer. Many of the commands described here serve as examples and may not yet be implemented in the current version of the tool.

## CLI Interface Design

- **Conversational**: Commands read like natural instructions
- **Discoverable**: Easy to find what you need with `help`
- **Extensible**: Seamlessly integrate new benchmark types
- **Consistent**: Predictable structure across different benchmark types

### Global Options

These options apply to all odometer commands:

```sh
odometer --version / -v     # Show application version
odometer --help / -h        # Display help information
odometer --debug            # Enable verbose debugging output
```

### Command Structure

The command structure follows the pattern: `odometer <verb> <noun> [options]`

```sh
odometer measure gas-limit  # Measure block gas limit
odometer list clients       # List available clients
odometer show results       # Display benchmark results
```

## Command Reference

### 1. Global Commands

```sh
odometer help      # Shows main help message with available commands
odometer version   # Displays Odometer version information
odometer debug     # Enables verbose debugging output
```

### 2. Primary Actions

#### A. Measure Benchmarks

```sh
odometer measure gas-limit [OPTIONS]
  --for <client1,client2,...>        # Optional: Clients to benchmark (default: all)
  --duration <seconds> / -d          # Optional: Test duration (default: 60)
  --rate <tps> / -r                  # Optional: Target transactions per second
  --output <format> / -o             # Optional: Output format (table, json, csv)
  --parallel <num_threads> / -p      # Optional: Concurrency level (default: 1)
  --config <file_path>               # Optional: Custom configuration file
  --endpoint <client>=<url>          # Optional: Override default RPC endpoint
```

Example:

```sh
odometer measure gas-limit --for geth,erigon --duration 120
```

#### B. List Available Resources

```sh
odometer list clients [OPTIONS]          # List configured Ethereum clients
```

Options:

```sh
  --verbose / -v     # Show detailed information
```

#### C. Show Detailed Information

```sh
odometer show results gas-limit [run_id | --latest] [OPTIONS]   # Display gas-limit benchmark results
odometer show client <client_name>                              # Show client configuration
```

Options:

```sh
  --output <format> / -o     # Specify output format
```

#### D. Configure System Components

```sh
odometer configure client add <name> --rpc-url <url> [OPTIONS]    # Add client
odometer configure client remove <name>                           # Remove client
```

## Future Extensibility

The command structure allows easy addition of new benchmark types:

```sh
odometer measure zkevm --for geth --test-cases proof_generation_time
odometer list clients zkevm
odometer show results zkevm
```
