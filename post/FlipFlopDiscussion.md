---
layout: default
title: Discussion on Filp Flop
---

## Discussion on Flip Flop: How to analyze the one's catching issue?

> Disclaimer: The content presented here is primarily based on my personal understanding and references. It should not be interpreted as a formal or definitive explanation.

#### Problem Definition

Let's begin by clearly defining the "Catching One Problem." A relevant question on Stack Exchange provides a good starting point: [Understanding the 1's catching problem in master-slave flip-flops](https://electronics.stackexchange.com/questions/136278/can-someone-explain-to-me-what-the-1s-catching-problem-is-in-the-master-slave-fl).

Consider the following logic simulation:

![Logic Simulation Figure for the issue](https://github.com/YardRat0117/picx-images-hosting/raw/master/catchingOne.51ee2gnr6f.webp)

In the figure, the area circled in red highlights a brief, unwanted pulse, namely a "glitch", on the `R` (Reset) signal. Due to the glitch, the output `Y` is erroneously reset. It then remains in this incorrect state for the remainder of the clock period, until the subsequent `S` (Set) signal eventually corrects it.

#### Analysis Definition

To better analyze this behavior, we can introduce two properties to describe actions or events: **instantaneous** and **continuous**.

- An **instantaneous** action occurs at a specific point in time, with negligible duration. For example, *closing a book* is approximately an instantaneous action.

- A **continuous** action extends over a period. For example, *reading a book* is a continuous action.

With these properties defined, we can understand why a level-triggered S-R master-slave flip-flop is susceptible to such glitches.

The "writing" process, or more accurately, the period during which the master latch is receptive to inputs, is effectively **continuous** as long as the clock signal `C` is `high`.

Consequently, an **instantaneous** glitch on an input (like `R`) occurring at any point during this "open window" can incorrectly alter the state of the master latch. This incorrect state is then faithfully passed to the slave latch when the clock changes state.

For a more intuitive illustration, imagine a notebook left open on a park bench, with a pencil and eraser nearby.

- The **notebook being open** is analogous to the clock signal `C` being `high`, making the master latch transparent.

- As long as the notebook is open, **anyone passing by** (representing an input glitch on `S` or `R`) can write in it or erase content.

- This can happen at **any instant** while the notebook is open.

- The information in the notebook when it's finally closed (when the clock `C` goes `low` and the master's state is passed to the slave) might not be what was intended, due to these transient modifications.

This analogy helps visualize how the continuous "write-enabled" period of the master latch makes it vulnerable to instantaneous disturbances.


#### Solutions Inspired by the Analogy

The notebook analogy not only clarifies the problem but also hints at potential solutions. How do we protect the notebook's integrity?

1. Continuously Dictate the Content (Minimizing Ambiguity): Instead of separate "Set" (write a '1') and "Reset" (write a '0') instructions that could be glitched, what if we continuously provide the *exact, complete page content* we want? This is akin to using a **D-type (Data) input**.

    - Analogy: Imagine you're not just leaving a pencil for anyone to write "set" or "reset" notes. Instead, you're constantly holding a complete, correct page template against the notebook. If the notebook is open (clock is high for a D latch), it reflects this template.

    - Flip-Flop Implementation (D Latch/Flip-Flop): With a `D` input, the flip-flop aims to store the value present at `D`. This simplifies the input logic compared to S-R inputs, eliminating the problematic `S=R=1` state and reducing the chances of conflicting transient signals on separate control lines causing an unintended flip. While a simple `D` *latch* is still transparent when the clock is high (and thus can catch glitches on `D` itself during this phase), the D-type input structure is foundational. The true robustness comes when combined with edge-triggering.

2. Lock the Notebook (Restricting Access Time): The most effective way to prevent unauthorized revisions is to keep the notebook locked and only open it for the briefest possible moment when a deliberate change is needed. This is the principle behind **edge-triggered flip-flops**.

    - Analogy: You only unlock and open the notebook for an instant (at the "edge" of a moment), write the new content, and immediately lock it again. Passersby (glitches) who arrive before or after this brief instant find the notebook locked and cannot alter its contents.

    - Flip-Flop Implementation (Edge-Triggering): Edge-triggered flip-flops (e.g., D flip-flops, JK flip-flops) only sample their inputs and change their output state at the specific moment of a clock transition (either rising edge or falling edge). This dramatically reduces the "vulnerability window" from the entire duration of the clock pulse being `high` (as in a level-sensitive latch) to a very short period defined by the clock edge and the flip-flop's setup and hold times. This is the primary mechanism to overcome the 1's catching problem as described.

#### Discussion on Robustness and Potential Exceptions

By moving to edge-triggered designs, especially edge-triggered D flip-flops, we significantly enhance robustness against the 1's catching issue. The "continuous exposure" problem is largely solved.

**But are there any exceptions?** One might ask: what if a glitch on the data input (`D`) occurs *exactly* at the clock edge, during that tiny window when the "notebook is briefly opened"?

- This scenario relates to **setup and hold time violations**. Setup time is the minimum time the data input must be stable *before* the active clock edge. Hold time is the minimum time the data input must remain stable *after* the active clock edge.

- If a glitch violates these timings, the flip-flop's output can become unpredictable or enter a **metastable state** (an undecided, oscillatory, or intermediate state that is neither a clear '0' nor a clear '1') before eventually settling.

- While this is a critical concern in digital design, it's a slightly different issue than the classic "1's catching" problem caused by glitches on `S`/`R` lines during the master latch's transparent phase. Edge-triggering effectively solves the latter by minimizing the transparent window. The challenge then becomes ensuring clean data around the clock edge.

- Statistically, a random input glitch perfectly aligning with the very narrow setup/hold window around the clock edge is less frequent than a glitch occurring during the much longer "clock high" phase of a level-sensitive latch. Modern design practices focus on ensuring data stability around clock edges to mitigate metastability.

Thus, while no system is immune to all possible signal integrity problems, edge-triggering is a fundamental and highly effective solution to the 1's catching problem discussed. You can refer to this simulation, note that the highlighted yellow timing point indicates a non-trivial "glitch", that, hit right in the head of positive edge of the clock pulse, and altered the `q` signal indeed. 

![Circuit Simulation for D-FlipFlop](https://github.com/YardRat0117/picx-images-hosting/raw/master/exception.1e8uft87la.webp)

#### Conclusion

In essence, the "1's catching problem" highlights a fundamental vulnerability in level-sensitive latches: their continuous period of transparency makes them susceptible to erroneous state changes caused by transient input glitches. As we've explored using the notebook analogy, this susceptibility can lead to unreliable behavior in digital circuits.

The transition to **edge-triggered flip-flops** stands as the cornerstone solution, drastically minimizing the "open window" for glitches by restricting input sampling to the precise moment of a clock edge. While nuances like setup and hold times introduce their own set of critical timing considerations, primarily concerning data stability around that edge, the core issue of catching stray pulses during a prolonged active clock phase is effectively addressed.
