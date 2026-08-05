### 2. Update `Piret bottlneck.md`
This expanded diagram maps the full illicit supply chain. It shows exactly how the stream is stolen, re-encoded on cheap hardware, and why the single-server egress gets crushed under the weight of public internet routing.

```markdown
# The Centralized Bottleneck: Pirated Stream Architecture

This diagram maps the structural failure points of an illicit streaming supply chain. Because these networks cannot utilize enterprise edge routing or auto-scaling containerization, they inevitably collapse at the ingestion, processing, or egress tiers during massive global demand.

```mermaid
graph TD
    subgraph "The Ingestion & Processing Bottleneck"
        LegitFeed[Legit Broadcaster Output] --> Capture[Hardware Capture / Screen Scrape]
        Capture --> DRMStrip[DRM Stripping Layer]
        DRMStrip --> CPU[Overloaded VPS: FFmpeg Re-encoding]
        CPU -->|Forces Single Bitrate| StreamOut[Rigid 1080p Output]
    end

    subgraph "The Routing & Egress Bottleneck"
        StreamOut --> NGINX[Static Reverse Proxy]
        NGINX --> Offshore[Single Offshore Media Server]
        Offshore -->|Bandwidth Cap Reached| ISP1[Public BGP Routing Hop 1]
        ISP1 --> ISP2[Public BGP Routing Hop 2]
        ISP2 --> ISP3[Public BGP Routing Hop 3]
    end

    subgraph "The Viewer Impact"
        ISP3 --> U1[Viewer 1: High Latency]
        ISP3 --> U2[Viewer 2: Packet Loss]
        ISP3 --> UN[Viewer 100,000+: Stream Crash]
    end
    
    classDef critical fill:#ffebee,stroke:#c62828,stroke-width:2px;
    classDef warning fill:#fff8e1,stroke:#f57f17,stroke-width:2px;
    classDef standard fill:#eeeeee,stroke:#616161,stroke-width:1px;
    
    class CPU,NGINX,Offshore critical;
    class Capture,DRMStrip,ISP1,ISP2,ISP3 warning;
    class LegitFeed,U1,U2,UN standard;
