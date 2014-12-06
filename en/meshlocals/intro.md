# Mesh Local Intro

## What is a Mesh Local?

A 'Mesh Local' is a mesh network situated in a particular geographic locale, focused on providing a community-centric alternative (or complement) to the internet.

## How local is local?

Project Meshnet's mesh networking protocol (cjdns) was designed to be agnostic of the medium over which it communicates. That means that even if the closest node is beyond the functional range of radio signals, you can still peer with it over the internet.

While this is useful for connecting with others who are interested, and for forming a seed from which a local network can grow, it relies on another network to exist. The ultimate goal is to create a net which will not fail if the internet does.

<div class="mermaid">
    graph LR;
        A(Local node)--\>|wireless lan cable|B(Other local node);
        B--\>A;
</div>

**NOTE**: If you're viewing this on a web page which does not include [mermaid.js](https://github.com/knsv/mermaid), you'll just see some weird text. For an example of how it **should** look, see it in [its original context](https://docs.meshwith.me/en/meshlocals/intro.html).
