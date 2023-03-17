#azure #az-204 

| Type             | Service                                         | Performance       | Access             | Replication                          | Deployment Models         |
| ---------------- | ----------------------------------------------- | ----------------- | ------------------ | ------------------------------------ | ------------------------- |
| Gen Purpose V1   | Blob, File, Queue, Table, Disk                  | Standard, Premium | N/A                | LRS, GRS, RA-GRS                     | Resource Manager, Classic |
| Gen Purpose V2   | Blob, File, Queue, Table, Disk, Data Lake Gen 2 | Standard, Premium | Hot, Cool, Archive | LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS | Resource Manager          |
| BlobStorage      | Blob (block, append)                            | Standard          | Hot, Cool, Archive | LRS, GRS, RA-GRS                     | Resource Manager          |
| BlockBlobStorage | Blob (block, append)                            | Premium           | N/A                | LRS, ZRS                             | Resource Manager          |
| FileStorage      | File                                            | Premium           | N/A                | LRS, ZRS                             | Resource Manager          |
