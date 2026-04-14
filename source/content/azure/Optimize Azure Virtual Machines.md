---
title: "Optimize Azure Virtual Machines"
tags:
  - azure
  - az-900
  - cost-optimization
  - virtual-machines
---

# Optimize Azure Virtual Machines

Use average resource utilization to judge whether [[Azure Virtual Machines]] are **oversized** (waste and cost), **right-sized**, or **undersized** (risk of saturation).

## Utilization heuristics

| Average usage | Interpretation |
|---------------|------------------|
| **Below ~10%** of provisioned capacity | Likely waste; consider smaller SKUs, fewer VMs, or consolidation. |
| **Around ~90%** | Often a healthy steady state if headroom still handles bursts. |
| **Above ~90%** sustained | Risk of performance issues; spikes may queue or fail when the VM is fully busy. |

If utilization is consistently too high or too low, adjust [[Virtual Machines size]] or architecture (for example scale out).

## Tools and purchasing options

- **[[Azure Advisor]]** analyzes VM usage over about **14 days** and surfaces recommendations. Example thresholds sometimes used as rules of thumb: **CPU under ~5%** or **network under ~7 MB/s** can indicate an **underutilized** VM where downsizing or removal may save cost.
- **Azure Reserved Virtual Machine Instances**: commit to **one- or three-year** capacity for a discount compared to pay-as-you-go list pricing for eligible VM families and regions (share benefits across matching usage in your billing scope per your reservation configuration).
