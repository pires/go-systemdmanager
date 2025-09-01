# go-systemdmanager

A Go library for managing systemd units via D-Bus API with OpenTelemetry instrumentation.

## Overview

This library provides a clean interface for controlling systemd units through D-Bus, supporting operations like start, stop, restart, uptime monitoring, and real-time status watching. It's designed with observability in mind, featuring comprehensive OpenTelemetry tracing and metrics.

## Features

- **Unit Lifecycle Management**: Start, stop, and restart systemd units
- **Status Monitoring**: Watch unit status changes in real-time
- **Uptime Tracking**: Retrieve unit uptime information
- **Observability**: Built-in OpenTelemetry instrumentation for tracing and metrics
- **Thread Safety**: Concurrent-safe operations with proper locking

## Usage

```go
import "github.com/pires/go-systemdmanager"

// Create a new manager
mgr, err := systemdmanager.New(ctx)
if err != nil {
    log.Fatal(err)
}

// Start a unit
err = mgr.Start(ctx, "my-service.service")

// Watch for status changes
updatesChan := make(chan *dbus.UnitStatus)
go mgr.Watch(ctx, "my-service.service", updatesChan)

// Get uptime
uptime, err := mgr.Uptime(ctx, "my-service.service")
```

## Requirements

- Go 1.24+
- Linux with systemd
- D-Bus access

## Credits

This project evolved from:

- [virtual-kubelet/systemk](https://github.com/virtual-kubelet/systemk) - Virtual Kubelet systemd provider
- [firedancer-io/mirasol](https://github.com/firedancer-io/mirasol) - Solana RPC watchdog
