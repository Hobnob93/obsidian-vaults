#azure #az-204 

**Queues** can be accessed by using the following URL format:
- https://`<storage account>`.queue.core.windows.net/`<queue>`
- e.g. https://myaccount.queue.core.windows.net/images-to-download

**Storage Account** is required for all Azure Storage access.

**Queue** contains a set of messages.
- The queue name must be all lowercase!

**Message** can be up to 64 KB, and in any format.
- Messages have an expiry of any positive number - default is 7 days
- You can set the expiry to -1 to indicate it never expires
- Prior to version **2017-07-29**, there was a maximum expiry of 7 days