# Parcel Document File Format

***Actual file foramt is subject to change, consult ParcelDocument class for latest accurate definition.***

Portability is of the greatest concern and despite many of the reference-based external resource referencing of certain functional nodes, all main data (including annotation) are embedded directly within a single Parcel document.

Parcel document is stored as a LZ4 compressed binary archive serialized in binary little endian, the compression library being used is [K4os.Compression.LZ4](https://github.com/MiloszKrajewski/K4os.Compression.LZ4). All core components of Parcel are written in **.Net Standard 2.0** and **Python 3.7**. The remaining of this document assumes an uncompressed flattened representation of the binary data.

For comprehensive definition and convinience of understanding, the official implementation of [ParcelDocument](.) saving and loading have explicitly defined all identifying fields in the document data format class, even though technically speaking those are non-essential information during runtime.

## General Structure

The general structure of the Parcel Document looks like this:

1. Identification and global document information
2. Number of graphs and graph data
3. Number of payloads and payload data
4. Number of caches and cache data
5. Change log

Below table shows the general structure:

| Type | Size | Name/Meaning |
| --- | --- | --- |
| string | *variable* | Type Name |
| string | *variable* | Version Name |
| int64 | 8 bytes | GUID Counter |
| int | 4 bytes | Number of Graphs |
| Graph | *variable* | Graph Data |
| ... | ... | ... |
| int | 4 bytes | Number of Payloads |
| Payload | *variable* | Payload Data |
| ... | ... | ... |
| int | 4 bytes | Number of Caches |
| Cache | *variable* | Cache Data |
| ... | ... | ... |
| Change Log | *variable* | Change Log |

## Node Data

Everything in Parcel is defined as a node. Nodes are considered document-wise resources and have a unique GUID throughout the lifetime of a document, which provides tracking of changes. There are four main types of nodes:

1. Parcel/Document/Language Construct
2. Primitives and Operators
3. Main Node Functions
4. Annotations

The main data for a node is simple: it consists of GUID, node type, and **node command**. The essence of node definition are provided through node commands - which are simply textual command-line formatted descriptions of nodes.

All commands generally share the basic same format: `<Command Name> <Node Position> <Command Parameters>`

## Binary Payloads

