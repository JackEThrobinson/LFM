<!-- [![Multi-Modality](agorabanner.png)](https://discord.com/servers/agora-999382051935506503) -->

# Liquid Foundation Models [LFMs]

[![Join our Discord](https://img.shields.io/badge/Discord-Join%20our%20server-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/agora-999382051935506503) [![Subscribe on YouTube](https://img.shields.io/badge/YouTube-Subscribe-red?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@kyegomez3242) [![Connect on LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kye-g-38759a207/) [![Follow on X.com](https://img.shields.io/badge/X.com-Follow-1DA1F2?style=for-the-badge&logo=x&logoColor=white)](https://x.com/kyegomezb)

**Welcome to the open-source implementation of Liquid Foundation Models (LFMs)** — the next generation of multi-modal, adaptive AI systems. LFMs represent a breakthrough in model architecture design, specifically tailored to meet the evolving demands of real-world applications across different modalities such as text, audio, image, and video. [The article provides some implementation details](https://www.liquid.ai/liquid-foundation-models)


## Installation
```bash
$ pip3 install -U lfm-torch
```

## Usage

```python
import torch
from lfm_torch.model import LFModel
from loguru import logger

# Instantiate and test the model
if __name__ == "__main__":
    batch_size, seq_length, embedding_dim = 32, 128, 512
    token_dim, channel_dim, expert_dim, adapt_dim, num_experts = (
        embedding_dim,
        embedding_dim,
        embedding_dim,
        128,
        4,
    )
    model = LFModel(
        token_dim, channel_dim, expert_dim, adapt_dim, num_experts
    )

    input_tensor = torch.randn(
        batch_size, seq_length, embedding_dim
    )  # 3D text tensor
    output = model(input_tensor)
    logger.info("Model forward pass complete.")
```


## Liquid Transformer 
Integrating transformers with lfms + mixture of experts. Very experimental and early!


```python
import torch
from loguru import logger

from lfm_torch.liquid_t_moe import LiquidTransformer

# Example usage
if __name__ == "__main__":
    seq_len, batch_size, embed_size = 10, 2, 64
    num_heads, num_experts, expert_size, num_layers = 8, 4, 64, 6

    # Create the model
    model = LiquidTransformer(embed_size, num_heads, num_experts, expert_size, num_layers)

    # Example input tensor
    x = torch.randn(seq_len, batch_size, embed_size)

    # Forward pass
    output = model(x)
    logger.info(f"Model output shape: {output.shape}")
```