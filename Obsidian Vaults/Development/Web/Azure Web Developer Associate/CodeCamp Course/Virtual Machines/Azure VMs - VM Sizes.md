#azure #az-204 

Azure VMs come in a variety of sizes optimised for specific use cases.
Azure VMs are grouped into:
- **Types** e.g. General Purpose, Compute Optimised
- **Sizes** e.g. B, Dsv3 (a.k.a. Series or SKU Family)

Some sizes may not be available depending on the image that you have chosen.
This is due to sizes being optimised for certain images.

**General Purpose**
Balanced CPU-To-Memory ratio.
Testing and development, small to medium databases, and low to medium traffic web servers.
**SKUs**: B, Dsv3, Dv3, Dasv4, Dav4, DSv2, Dv2, Av2, DC, DCv2, Dv4, Dsv4, Ddv4, Ddsv4

**Compute Optimised**
High CPU-to-memory ratio.
Good for medium traffic web servers, network appliances, batch processors, and app servers.
**SKUs**: F, Fs, Fsv2

**Memory Optimised**
High memory-to-CPU ratio.
Great for relational database servers, medium to large caches, and in-memory analytics.
**SKUs**: Esv3, Ev3, Easv4, Eav4, Ev4, Esv4, Edv4, Edsv4, Mv2, M, DSv2, Dv2

**Storage Optimised**
High disk throughput and IO.
Ideal for Big Data, SQL, NoSQL databases, data warehousing, and large transactional databases.
**SKUs**: Lsv2

**GPU Specialised**
Heavy graphic rendering and video editing, model training and inferencing (ND) with deep learning.
Available with single or multiple GPUs.
**SKUs**: NC, NCv2, NCv3, NCasT4_v3 (Preview), ND, NDv2 (Preview), NV, NVv3, NVv4

**High Performance Compute**
Fastest and most powerful CPU VMs with optional high-throughput network interfaces (RDMA).
**SKUs**: HB, HBv2, HC, H