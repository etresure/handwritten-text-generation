# handwritten-text-generation

## pair (two images from the same writer)

```mermaid
flowchart LR
  %% Two samples of same writer
  subgraph A["Sample A"]
    XS["Image x_style"]
    TS["Text t_style"]
    WS["ID writer_id"]
  end
  %% Encoder
  XS --> E["Style encoder E(x)"]

  subgraph B["Sample B"]
    XT["Image x_target"]
    TT["Text t_target"]
    WT["ID writer_id"]
  end

  %% Model
  TT --> G["Diffusion model G(t_target, s)"]

  %% Style vector
  E --> S["Style embedding s"]
  S --> G

  %% Output
  G --> XH["Generated image xhat_target"]

  %% Loss
  XH --> L["Loss: compare xhat_target to x_target"]
  XT --> L

  style E fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  style G fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  style L fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  ```

## single (one image)

```mermaid
flowchart LR
  %% Single-sample setup
  subgraph A["Sample A"]
    X["Image x"]
    T["Text t"]
    WS["ID writer_id"]
  end
  X --> E["Style encoder E(x)"]
  T --> G

  %% Style
  E --> S["Style embedding s (capacity-limited)"]
  S --> G["Diffusion model G(t, s)"]

  %% Output
  G --> XH["Generated image xhat"]

  %% Loss
  XH --> L["Loss: compare xhat to x"]
  X --> L

  style E fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  style G fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  style L fill:#b8e2f2,stroke:#2c6b9c,stroke-width:2px,color:#000000
  ```