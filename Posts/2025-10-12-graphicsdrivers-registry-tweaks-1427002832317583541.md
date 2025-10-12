---
title: "# GraphicsDrivers Registry Tweaks"
author: "pppp1116"
date: "2025-10-12T18:39:47.655Z"
source: "https://discord.com/channels/1375751335428882492/1376156106174234677/1427002832317583541"
category: "tweaks"
tags: []
---
# GraphicsDrivers Registry Tweaks

This `.reg` file applies a set of reverse-engineered Windows graphics driver settings. These values were identified through static analysis of core system components (`dxgkrnl.sys`, `win32kfull.sys`) using IDA. They affect GPU P-state control, D3 power transition latency thresholds, and low-level DMA/IOMMU behavior.

## Overview

- **DisablePStateManagement / DisableDevicePowerRequired**  
Control the GPU’s performance state management and power requirement behavior. Disabling P-state management keeps the GPU at higher clocks more consistently.

- **DefaultD3Transition* Thresholds and Latencies**  
These keys govern how long the system waits before transitioning the GPU to low-power D3 state, and how much latency is added once idle. Increasing these values reduces aggressive downclocking and sleep transitions, improving responsiveness during short idle periods.

- **Smm Subkey (IdentityMappedPassthrough / ForceDmaRemapping / ForceEnableIommu)**  
These modify how the GPU interacts with the system’s IOMMU and DMA remapping. Enabling identity-mapped passthrough and forcing IOMMU can lower latency in some scenarios and alter how the GPU accesses memory.

## Notes

- These settings are **not documented by Microsoft** and may behave differently depending on Windows version and GPU driver.  
- They were found in code paths related to registry lookups (e.g., `FastGetProfileDword`) inside the Windows graphics stack.  
- A system reboot is required after applying the `.reg` file for the changes to take full effect.  
- Intended for advanced users and testing on performance-tuned systems.

## Anexos
- [d3.reg](https://github.com/Pppp1116/knowledge-base/blob/main/attachments/1427002832317583541/d3.reg)
