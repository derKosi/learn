
:::image type="content" source="../media/middleware-stack.png" alt-text="Diagram showing the different parts of the quantum stack middleware layer.":::

The middleware layer intermediates between the high-level applications submitted over the cloud and the underlying hardware. This layer naturally covers a broad range of areas and domains, including communications, resource management, security, and compilation. Here's a sketched, nonexhaustive list of some core components of this middleware layer. It's followed by a brief look at key areas of software development within the quantum stack.

## Compilers

QPUs, like CPUs, run on instruction sets. Therefore, once a job is received, it must be compiled into low-level instructions that the quantum computer understands. Since the QPUs under development can have different hardware underlying their operation, instruction sets are often specific to hardware platforms and vendors.  

Therefore, it's important to have fast and efficient compilers that can take a high-level language and compile it into a native instruction set. Simply translating isn't enough, though. By intelligently optimizing the quantum program, which again can be dependent on the QPU architecture, the quantum program can be made to run faster and more efficiently, with fewer errors.

Therefore, building smart compilers is an active area of work and an important part of the quantum computing stack.  

## Calibration

Quantum computers are delicate and complex machines. They have a vast number of components, each sensitive to its environment. The slightest temperature change can mean the difference between getting the right or wrong answer.  

Therefore, software plays a significant role in monitoring the QPU’s performance and how it changes over time to ensure it always works optimally.  

## UI & Data management

As you can imagine, running a machine as complex as a quantum computer continually produces a large volume of data, along with machine settings, parameters, and metrics. All of this information needs to be handled, recorded, analyzed, and reported to the operators. Effectively building these tools aids scientists and engineers in gaining critical insights into their operation and facilitates real-time monitoring and debugging.  

These are just a few of the software tasks involved at the software layer, but I think you'll appreciate that the actual number of responsibilities is too long to discuss here. We hope this gives you a flavor of some of the roles of the software layer.
