# The ROS 2 Launch System

The launch system in ROS 2 is responsible for helping the user describe the configuration of their system and then execute it as described.
The configuration of the system includes what programs to run, where to run them, what arguments to pass them, and ROS specific conventions which make it easy to reuse components throughout the system by giving them each different configurations.
It is also responsible for monitoring the state of the processes launched, and reporting and/or reacting to changes in the state of those processes.

The ROS 2 Bouncy release includes a framework in which launch files, written in Python, can start and stop different nodes as well as trigger and act on various events.
The package providing this framework is `launch_ros`, which uses the non-ROS-specific `launch` framework underneath.

The [design document (in review)](https://github.com/ros2/design/pull/163) details the goal of the design of ROS 2's launch system (not all functionality is currently available).
## Example of ROS 2 launch concepts

The launch file in [this example](https://github.com/ros2/launch/blob/master/launch_ros/examples/lifecycle_pub_sub_launch.py) launches two nodes, one of which is a node with a [managed lifecycle](https://github.com/ros2/ros2/wiki/Managed-Nodes) (a "lifecycle node").
Lifecycle nodes launched through `launch_ros` automatically emit _events_ when they transition between states.
The events can then be acted on through the launch framework, e.g. by emitting other events (such as requesting another state transition, which lifecycle nodes launched through `launch_ros` automatically have event handlers for) or triggering other _actions_ (e.g. starting another node).

In the aforementioned example, various transition requests are requested of the `talker` lifecycle node, and  its transition events are reacted to by, for example, launching a `listener` node when the lifecycle talker reaches the appropriate state.

## Usage

While launch files can be written as standalone scripts, the typical usage in ROS is to have launch files invoked by ROS 2 tools.

For example, [this launch file](https://github.com/ros2/demos/blob/master/demo_nodes_cpp/launch/services/add_two_ints.launch.py) has been designed such that it can be invoked by `ros2 launch`:

```bash
ros2 launch demo_nodes_cpp add_two_ints.launch.py
```

## Documentation

[The `launch` documentation](https://github.com/ros2/launch/blob/master/launch/doc/source/architecture.rst) provides more details on concepts that are also used in `launch_ros`.

Additional documentation/examples of capabilities are forthcoming.
See [the source code](https://github.com/ros2/launch) in the meantime.