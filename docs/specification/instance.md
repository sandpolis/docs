# Instance
The following sections apply to all Sandpolis instances.

## Data Model
There are three layers in the Sandpolis data model. Of which, client implementations
are required to support at least two (ST and OID layers).

### The ST Layer
The State Tree layer is the lowest layer and is concerned with storage and persistence.
Every instance maintains a global tree called the "ST Tree". The tree is seldomly
manipulated directly. Instead, higher layers make changes to the ST Tree on behalf
of consumers.

The ST tree is composed of two components: `Attribute`s and `Document`s.

#### Attributes
Attributes contain data of a specific type and meaning. All data in the ST tree is
stored in attributes.

The history of an attribute can optionally be recorded with _tracked attributes_.

#### Documents
Documents are a set of attributes and sub-documents.

#### Entanglement
A concept that exists at the ST layer is **entanglement**: ST trees that reside
on remote instances can synchronize their state. The relation can be bidirectional
or unidirectional and last as long as necessary. All changes to the source of an
entanglement pair will be propagated to the destination in real-time.

#### Change Events

#### Snapshots and Merging


### The VST Layer

### The OID Layer
Every node in a ST Tree is uniquely identified by an OID. OIDs are sequences of `/`
separated strings that describe how to reach the corresponding node from the root
node. OIDs also have a string namespace identifier that identifies the plugin or
module to which the OID belongs.
