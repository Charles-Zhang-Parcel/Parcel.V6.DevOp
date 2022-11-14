# Software Architecture

* Excel Addin supports maximum .Net version as .Net Framework 4.8, thus for Excel-native hosted graph editor experience, we should target our entire solution to Netstandard 2.0, including the GUI parts - fortunately SFML is built on top of Netstandard 2.0.

## Node Command

The cononical node command format: `<Fully Qualified Node Name> <Node Position> <Display Name> [<Node Input Names and Output Names>]`.  
Node instances DO NOT need an instance/display/variable name, because as per the final code-generation, we never refer to nodes themselves but refer directly to their input and outputs which are defined as variables. Node instances generally are referred to by fully qualified functional names in the case of Parcel (think of it as a line of actual C# code), but we do provide a way to override display name - just like in Terragen.

The design of nodes is such that it's as close and as a think wrapper over the actual underlying "code" or function as possible, so nodes are not even real "objects" from an OOP perspective (contrary to earlier designs of Parcel, e.g. Parcel V2). Essentially, most of the parameters are shown in the "connonical node command format" is just for "decoration purpose" - for the correct display of the node in the GUI and identifying of the corresponding functions. The real and more essential information regarding a node is simply: what function is it calling, and how are the inputs and outputs identified.

Code generation from node commands are trivial:

1. For native C# code, we just call make sure corresponding namespaces are being declared and involved modules are involved, then we declare the variables and make the calls.
2. For Python code, we either generate python code and make calls, or wrap nodes involving python calls with proper Pythonnet calling pattern.

### Node Input Names and Output Names

This optional argument defines all the named input and output variables are used by the node. All such variables share a single namespace within a particular graph.

Node inputs and outputs can be either:

1. Plain literal values;
2. Variable names.

Primitive nodes takes no input and produces a single output, other nodes might take both inputs and generate outputs. Names as `_` meaning "discarded" or not being used by other nodes.

## Graph Types

Graph Types defines the data representation of the underlying node constructions, as stored in the Parcel document file; The GUI rendering, however, might choose the appropriate way to present things which blurs the line of distinct graph types. For instance, it's possible to directly see all grpah content of a Flow Chart context within any containing graph without having to open the flow chart context as a distinct cavnas screen. The same applies to an Execution Graph.

### Functional Graph

**Functional graphs** do not contain control flows. There will be functional nodes that provides similar functionalities, i.e. operations on lists or arrays of objects.

### Flow Chart Graph

### Execution Graph

The traditional imperative construct.