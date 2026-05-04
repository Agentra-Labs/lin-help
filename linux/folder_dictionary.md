# LINUX KERNEL TOP-LEVEL MAP

## CORE SYSTEM
- init/        → boot sequence, runs /init (your OS entry point)
- kernel/      → scheduler, process management, signals
- mm/          → memory management (paging, allocation)
- fs/          → virtual filesystem layer (files, mounts)

## HARDWARE + INTERFACE
- drivers/     → all hardware drivers (GPU, input, disk, network)
- arch/        → CPU-specific code (x86 boot, low-level ops)
- include/     → kernel headers (APIs, structs)

## SUBSYSTEMS
- net/         → networking stack (TCP/IP, sockets)
- ipc/         → inter-process communication
- io_uring/    → async I/O subsystem
- security/    → security layers (SELinux, etc.)
- crypto/      → cryptography

## GUI / USER INTERACTION
- drivers/gpu/     → graphics (DRM/KMS, display)
- drivers/input/   → keyboard, mouse, input devices
- sound/           → audio

## SUPPORT / INFRA
- lib/         → kernel helper functions
- scripts/     → build/config tools
- Documentation/ → official docs
- samples/     → example code

## SPECIAL / OPTIONAL
- rust/        → Rust support
- virt/        → virtualization (KVM, etc.)
- tools/       → debugging/profiling tools
- usr/         → initramfs embedding

## BUILD SYSTEM
- Makefile     → top-level build
- Kconfig      → config system (menuconfig)
- Kbuild       → build rules

## HOW TO DEBUG (MENTAL MAP)
- display issue        → drivers/gpu/
- keyboard/mouse       → drivers/input/
- boot crash           → init/ kernel/ mm/
- file problems        → fs/
- process issues       → kernel/
- memory issues        → mm/

