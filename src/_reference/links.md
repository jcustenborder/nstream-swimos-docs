---
title: Links
layout: page
redirect_from:
  - /concepts/links/
---

Central to programming is the ability to create pointers, or references, to things. Pointers are much more than memory addresses. Pointers often represent usage restrictions (think `const`, or `volatile`). And modern CPUs even use pointers as caching hints, pre-fetching data that might eventually be used in a computation. Swim takes the idea of pointers to the next level, enabling streaming references to the lanes of remote Web Agents, with strong consistency guarantees.

Native machine pointers also trigger transparent message passing between CPU cores on a computer's memory bus, to keep the machine's memory model in a consistent state. Similarly, links between Web Agents trigger transparent message passing between networked machines to keep Swim's distributed memory model consistent.

Links unify edges in an object graph, pointers in a cache coherency system, and subscriptions to mesaging topics, into a single, ultra high performance, easy to use programming primitive.

Links are bi-directional. Either end of a link can update its implicitly shared state in an eventually consistent manner. A link has a downlink side, and an uplink side. The **downlink** side is the one held by the endpoint that opened the link. The **uplink** side is the one held by the endpoint that received the link request.

To open a link, you create a downlink, and specify the address of the Web Agent (called the **node URI**), and the name of the lane (called the **lane URI**) to which you want to link. It's easier than it sounds. Here's what opening a link to a `ValueLane` looks like:

```java
const yourName = swim.downlinkValue()
.node("warp://example.com/person/you")
.lane("name")
.open();
```

Once you open a link, Swim automatically handles maintaining a network connection to the appriate machine, and transparently shuffles messages back and forth to keep the link in sync with the state of the remote lane.

Downlinks allow you to access a locally cached version of the remote lane's state, without blocking or waiting.

```java
console.log(yourName.get()); // prints your name
```

You can also set the state of a remote lane through a downlink.

```java
yourName.set("Yours Truly");
```

Conflicts are automatically resolved, and all links made eventually consistent. You can observe real-time state changes to remote lanes by registering callback functions on downlinks.

```java
yourName.didSet(name => console.log(`your name changed to ${name}`));
```

When you're no longer interested in the state of a remote lane, you can close a downlink to stop receiving updates.

```java
yourName.close();
```

Links are point-to-point, and unbuffered, making them real-time within the latency of the network and CPU.

Jump ahead to [Recon](/reference/recon) to find out how lanes and links represent data internally. Dive into the [tutorials](/tutorials) to see how links get used in a real application. Or read on to learn more about the different kinds of links, their properties, and their guarantees.

<!--<h2 class="header-green">Downlinks</h2>
<div class="feature-stack">
  <div class="feature-block feature-block-left">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>ValueDownlink</h3>
      <p></p>
    </div>
  </div>
  <div class="feature-block feature-block-right">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>MapDownlink</h3>
      <p></p>
    </div>
  </div>
  <div class="feature-block feature-block-left">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>ListDownlink</h3>
      <p></p>
    </div>
  </div>
</div>
<h2 class="header-green">Uplinks</h2>
<div class="feature-stack">
  <div class="feature-block feature-block-left">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>Uplink</h3>
      <p></p>
    </div>
  </div>
</div>
<h2 class="header-green">Link Modems</h2>
<div class="feature-stack">
  <div class="feature-block feature-block-left">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>Supply-driven links</h3>
      <p></p>
    </div>
  </div>
  <div class="feature-block feature-block-right">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>Demand-driven links</h3>
      <p></p>
    </div>
  </div>
  <div class="feature-block feature-block-left">
    <div class="feature-graphic">
    </div>
    <div class="feature-description">
      <h3>Supply and demand-driven links</h3>
      <p></p>
    </div>
  </div>
</div>-->

