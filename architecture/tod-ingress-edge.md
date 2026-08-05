# Enterprise Edge Ingress: TOD Architecture

This diagram illustrates how an enterprise platform utilizes edge routing and elastic Kubernetes scaling to absorb massive concurrent login spikes without crashing.

```mermaid
graph TD
    subgraph "Legitimate Enterprise Architecture (AWS Edge & EKS)"
        U1[Viewer] -->|Connects to Closest Edge Location| GA[AWS Global Accelerator / CloudFront]
        GA -->|Congestion-Free Private AWS Backbone| ALB[Application Load Balancer]
        ALB -->|Auto-Scales based on demand| EKS1[Amazon EKS Worker Node 1]
        ALB --> EKS2[Amazon EKS Worker Node 2]
        ALB --> EKS3[Amazon EKS Worker Node N...]
        EKS1 --> VOS[Harmonic VOS360 Video Processing]
        EKS2 --> VOS
    end
    
    classDef legit fill:#e1f5fe,stroke:#0288d1,stroke-width:2px;
    classDef edge fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px;
    
    class GA,ALB,EKS1,EKS2,EKS3,VOS legit;
    class U1 edge;
