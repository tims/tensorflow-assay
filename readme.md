# Notes on tensor flow

From [TensorFlow: A System for Large-Scale Machine Learning](https://www.usenix.org/system/files/conference/osdi16/osdi16-abadi.pdf).

## Design principles

* Dataflow graphs of primitive operators. Include multiplication and addition, this makes it easy to compose new types of complex layers. In addition to the functional operators, we represent mutable state, and the operations that update it, as nodes in the dataflow graph, thus enabling experimentation with different update rules.

* Deferred execution

* Common abstraction for heterogeneous accelerator. TensorFlow uses tensors of primitive values as a common interchange format that all devices understand.

The main consequence of these principles is that in TensorFlow there is no such thing as a parameter server.

## TensorFlow execution model

TensorFlow differs from batch dataflow systems (§2.3) in two respects:

* The model supports multiple concurrent executions on overlapping subgraphs of the overall graph.
* Individual vertices may have mutable state that can be shared between different executions of the graph.

Dataflow with mutable state enables TensorFlow to mimic the functionality of a parameter server, but with additional flexibility, because it becomes possible to execute arbitrary dataflow subgraphs on the machines that host the shared model parameters.


TensorFlow takes the best of parameter server and batch dataflow systems.

### Dataflow graph elements

* Tensors
* Operations
* Stateful operations: variables
* Stateful operations: queues
