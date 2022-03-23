#azure #azure-wda 

# Determine Appropriate Virtual Machine Size
Consider the type of workload your VM needs to run.
Based on workload, you're able to choose from a subset of VM sizes.
Workload options are classified as follows:
- `General Purpose`
	- Balanced CPU-to-memory ratio
	- Ideal for testing and development
	- Small to medium sized databases
	- Low to medium traffic web servers
- `Compute Optimised`
	- High CPU-to-memory ratio
	- Medium traffic web servers
	- Network appliances
	- Batch processes
	- Application servers
- `Memory Optimised`
	- High memory-to-CPU ratio
	- Relational database servers
	- Medium to large caches
	- In-memory analytics
- `Storage Optimised`
	- High disk throughput and IO
	- Big Data, SQL, NoSQL databases
	- Data warehousing
	- Large transactional databases
- `GPU`
	- Specialised VMs targeted for heavy graphic rendering
	- Video editing
	- Model training
	- Inferencing with deep learning
	- Available with single or multiple GPUs
- `High Performance Compute`
	- Fastest and most powerful CPU VMs
	- Optional high-throughput network interfaces (RDMA)

## What If Size Needs Changing?
*Azure* allows for a size change when current size no longer suits your needs.
Can resize VM as long as current hardware config is allowed in the new size.
Provides a fully agile and elastic approach to VM management.

if you stop and deallocate VM, you can select any size available in your region.
This removes your VM from the cluster in which it was running.