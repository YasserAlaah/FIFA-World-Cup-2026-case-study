# Enterprise Edge Ingress: TOD Architecture

This diagram details the full lifecycle of a user request and video delivery path during a high-concurrency sporting event. It highlights the separation of the authentication control plane (Amazon EKS) from the video data plane (Harmonic VOS360 and Multi-CDN).

```mermaid
graph TD
    subgraph "Edge Delivery & Security Tier"
        Viewers[Millions of Viewers] --> R53[Amazon Route 53 DNS]
        R53 --> CDN[Multi-CDN: AWS CloudFront / Akamai]
        CDN --> WAF[AWS WAF - DDoS & Bot Protection]
        WAF --> GA[AWS Global Accelerator]
    end

    subgraph "Routing & Authentication Tier"
        GA --> ALB[Application Load Balancer]
        ALB -->|Auto-Scales Horizontally| EKS1[EKS Worker Node: Auth Pods]
        ALB --> EKS2[EKS Worker Node: Routing Pods]
        ALB --> EKSN[EKS Worker Node: N...]
    end

    subgraph "State & Data Tier"
        EKS1 -.-> Redis[(Amazon ElastiCache / Redis)]
        EKS2 -.-> Redis
        EKS1 -.-> DB[(Amazon Aurora DB)]
    end

    subgraph "Video Processing Tier (Harmonic VOS360)"
        Broadcast[Clean Stadium Feed] --> Ingest[Cloud Ingest]
        Ingest --> ABR[Adaptive Bitrate Transcoding 4K/1080/720]
        ABR --> DRM[Synamedia DRM & Watermarking]
    end

    DRM -->|Pushes Chunks| CDN
    
    classDef edge fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px;
    classDef compute fill:#e1f5fe,stroke:#0288d1,stroke-width:2px;
    classDef data fill:#fff3e0,stroke:#e65100,stroke-width:2px;
    classDef video fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px;
    
    class Viewers,R53,CDN,WAF,GA edge;
    class ALB,EKS1,EKS2,EKSN compute;
    class Redis,DB data;
    class Broadcast,Ingest,ABR,DRM video;
