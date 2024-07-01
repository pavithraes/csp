## Table of Contents

- [Table of Contents](#table-of-contents)
- [Terms](#terms)
  - [Event stream processing](#event-stream-processing)
  - [Time Series](#time-series)
  - [Tick](#tick)
  - [Node (`csp.node`)](#node-cspnode)
  - [Graph (`csp.graph`)](#graph-cspgraph)
  - [Edge](#edge)
  - [Engine time](#engine-time)
  - [Alarm](#alarm)
  - [Adapter](#adapter)
  - [Wiring (Graph build-time)](#wiring-graph-build-time)
  - [Graph runtime](#graph-runtime)
  - [Baskets](#baskets)
  - [Dynamic graph](#dynamic-graph)

## Terms

### Event stream processing

The practice of processing continuous, real-time events.

Real-time events can be found everywhere, including mouse clicks on a website and weather data recordings. Processing these events as they change is valuable to gather meaningful insights and affect timely changes in other parts of the system.

### Time Series

Data that is tracked over a time period and indexed using timestamps.

Real-time events are often expressed as Time Series data. CSP works almost entirely with Time Series values, and other types of data are converted into Time Series values.

### Tick

A change in real-time events is called a "tick" in CSP.
Ticking [edge](#edge)s drive the flow of a CSP program.

The term "tick" is derived from [Stock Tickers](https://en.wikipedia.org/wiki/Ticker_symbol).

Some relevant `csp.node` operations:

- `csp.ticked` - returns `True` if a value has ticked
- `csp.valid` - returns `True` if a value has ticked at least once

### Node (`csp.node`)

Individual computing units of a CSP program are called nodes. They are defined as Python functions decorated with `csp.node` and are executed when a "ticking" condition is met.

Learn more in [CSP Node concepts](https://github.com/Point72/csp/wiki/CSP-Node).

### Graph (`csp.graph`)

A CSP graph consists of multiple connected nodes and describes a complete CSP workflow.

Python functions decorated with `csp.graph` create a graph. These are executed only once for constructing the graph. `csp.show_graph` can be used to view the constructed graph.

### Edge

Elements that connect nodes in a graph, and tick to trigger the execution of nodes.

You can manipulate Edges directly with some methods in [Functional Methods API](https://github.com/Point72/csp/wiki/Functional-Methods-API).

### Engine time

The CSP engine maintains an independent view of the current time, called the engine time. The current time of the engine can be accessed at any time within a `csp.node` by calling `csp.now()`.

### Alarm

A Time Series input set within a node. It can be scheduled to tick after a certain time interval.

Learn more in [Anatomy of a CSP node](https://github.com/Point72/csp/wiki/CSP-Node#anatomy-of-a-cspnode).

### Adapter

The mechanism to extend CSP's functionality.

Several common operations like support for different Input/Output data formats are implements as Adapters.

Learn more in [Adapters concepts](https://github.com/Point72/csp/wiki/Adapters)

### Wiring (Graph build-time)

CSP constructs a graph describing and setting-up the workflow before execution, this is called wiring or graph build-ime.

There are several CSP components that are only required during graph build time, especially when [writing your own adapters](https://github.com/Point72/csp/wiki/Write-Historical-Input-Adapters).

### Graph runtime

Execution of the pre-constructed graph by the CSP engine is called runtime.

### Baskets

A collection of Time Series values that can be passed in as a single argument. Individual values can tick independently, and can be processed individually or collectively. Baskets can either be `list` or `dict` type.

Learn more in [CSP Node concepts](https://github.com/Point72/csp/wiki/CSP-Node#basket-inputs)

CSP also has `DynamicBasket`s that can change their shape over time. Learn more in [Create Dynamic Baskets](https://github.com/Point72/csp/wiki/Create-Dynamic-Baskets).

### Dynamic graph

A graph that can change it's shape during execution.

Learn more [this dynamic graphs example](https://github.com/Point72/csp/blob/main/examples/06_advanced/e1_dynamic.py).
