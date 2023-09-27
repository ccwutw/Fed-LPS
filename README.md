# Fed-LPS

## Setting Up a Dask Distributed Cluster

If you're looking to set up a distributed computing environment using Dask, you'll primarily deal with two components: the **Scheduler** and the **Worker**.

### 1. **Scheduler**:
The scheduler orchestrates tasks and manages the workers. It acts as the central hub to which the workers connect.

To start the Dask scheduler, use the following command:

```bash
dask-scheduler
```

Upon execution, the scheduler will provide an address (e.g., `tcp://127.0.0.1:8786`). This is the address workers and clients will use to connect to the scheduler.

### 2. **Worker**:
Workers handle the actual computations. You can run multiple workers across various machines or cores.

To start a Dask worker, use the following command, replacing the address with that of the scheduler:

```bash
dask-worker tcp://127.0.0.1:8786
```

You can execute the `dask-worker` command on multiple machines or multiple times on a single machine to initiate multiple workers.

### 3. **Dask Client (Python Code)**:

Within your Python script, you'll need to connect to the scheduler:

```python
from dask.distributed import Client

# Connect to the Dask scheduler
client = Client('tcp://127.0.0.1:8786')
```

Replace `tcp://127.0.0.1:8786` with the actual address of your scheduler. After establishing the connection, you can execute the previously discussed LP code, allowing Dask to utilize the scheduler and workers to distribute tasks.

### 4. **Monitoring**:

One of the standout features of Dask is its diagnostic dashboard, which offers real-time feedback. When initiating the scheduler, it typically displays a dashboard link like `http://127.0.0.1:8787/status`. Opening this link in a web browser enables you to monitor task progression, worker status, and other pertinent metrics.

---

**Note**: This guide is tailored for a local cluster setup. For genuine distributed computing across multiple machines, ensure that the scheduler and workers are correctly networked. Also, firewall configurations should permit communication. When deploying Dask on cloud platforms or utilizing container orchestration tools like Kubernetes, more intricate configurations might be necessary.
