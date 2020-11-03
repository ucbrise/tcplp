TCPlp Benchmarking Code
=======================

This repository contains code that we used to produce the RIOT-OS/OpenThread throughput results for the paper:

Sam Kumar, Michael P Andersen, Hyung-Sin Kim, and David E. Culler. Performant TCP for Low-Power Wireless Networks. NSDI 2020.

The code is intended to help reproduce results presented in the paper. It is not intended to be used as a standalone TCP library. The code for TCP is primarily in `leaf_nodes/anemometer-qualified-fw/RIOT-OS/pkg/openthread/contrib`. You can find example usage in `leaf_nodes/anemometer-qualified-fw/app`. Running the code will require embedded hardware similar to what we used for our experiments. We use sensor nodes based on the Hamilton platform, each connected to a Raspberry Pi as a back channel, for our testbed. The Hamilton-based sensor nodes are similar to the SAMR21-XPRO.

The code for the leaf nodes, router nodes and border router node can be found in the respective directories. Inside `anemometer-qualified-fw/app`, running `make` and then `make flash` should build the code and flash the device via JLink.

For leaf nodes, look closely the `-DUSE_TCP`, `-DUSE_COAP`, `-DCOCOA`, etc. options. They can be used to control which options are used to send data over the network.

For the border router, use the `wpantund` program in the submodule. We use a simple reliability protocol over the serial link to communicate with `wpantund`. You should use the REthos (in `RIOT-OS/dist/tools/rethos`) program together with `stomp` (which converts REthos messages into a stream format for `wpantund`) to establish the connection with `wpantund`.
