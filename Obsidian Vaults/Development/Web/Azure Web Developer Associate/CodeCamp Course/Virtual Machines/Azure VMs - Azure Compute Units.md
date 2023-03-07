#azure #az-204 

Azure Compute Unit (**ACU**) provides a way of comparing compute (**CPU**) performance Across Azure VM Sizes (**SKUs**).

ACU is currently standardised on a **Small (Standard_A1)** VM with the value of ==100==.
All other SKUs then represent approximately how much faster that SKU can run a standard benchmark.

| SKU Family | ACU / vCPU | vCPU : Core Ratio |
| ---------- | ---------- | ----------------- |
| A1 - A4    | 100        | 1:1               |
| D1 - D14   | 160-250    | 1:1               |

D1 - D14 are 60% - 150% more performant than A1-A4.