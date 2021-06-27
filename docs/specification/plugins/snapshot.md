# Snapshot Plugin
The snapshot plugin gives agents the ability to take and apply snapshots, even
on filesystems that don't natively support snapshots.

## Block-based snapshots
The target device is divided into blocks of a configurable size. Each block has
a corresponding block hash which is the murmur3 128-bit hash 

## File-based snapshots

## Server
The server is responsible for storing snapshot data and uploading/downloading it
to/from agents.

### Snapshot format
Snapshot contents are stored in QEMU qcow2 files on the server. This format is
mature and supports useful features like compression and encryption.

## Agent

### Bootagent
A bootagent is responsible for reading/writing the actual data to/from the agent's
disks.

#### Residency
The bootagent runs in a minimized Alpine Linux environment.

#### Create Snapshot
If there exist no previous snapshots, the bootagent first determines the appropriate
block size for the disk. The agent may take into account the size of the disk or
the erase-block size of an SSD, but the block size must be a power of two.

If there exists a previous snapshot for the disk, the agent receives a stream of
block hashes. A single worker thread reads blocks from the disk and compares their hashes
against the block hashes retrieved from the server. If the hashes do not match,
the block is passed into a send queue to be egressed to the server.

#### Apply Snapshot
If there exists a previous snapshot for the disk, the agent initiates a stream of
block hashes. A single worker thread reads blocks from the disk and passes their
hashes into a send queue to be egressed to the server.

Simultaneously, the agent receives a stream of block data which are placed into
a write queue to be written to the device.
