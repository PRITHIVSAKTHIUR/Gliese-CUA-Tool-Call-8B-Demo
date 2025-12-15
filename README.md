# **Gliese-CUA-Tool-Call-8B-Demo**

> A Gradio-based demonstration for the prithivMLmods/Gliese-CUA-Tool-Call-8B model, a Computer Use Agent (CUA) specialized in GUI understanding and tool-calling actions. Users upload UI screenshots (e.g., desktop or app interfaces), provide task instructions (e.g., "Click on the search bar"), and receive parsed actions (e.g., clicks or types with coordinates) visualized as crosshairs and labels on the image. Outputs structured JSON tool calls within `<tool_call>` blocks for precise interactions.

## Features

- **GUI Action Inference**: Natural language tasks generate JSON-formatted tool calls (e.g., {"action": "click", "coordinate": [400, 300]}).
- **Action Visualization**: Overlays red crosshairs for clicks (or blue for others) with yellow labels on the output image using PIL.
- **Tool-Call Parsing**: Extracts actions from regex-matched `<tool_call>` blocks; supports coordinates and text inputs.
- **Efficient Processing**: Uses float16 precision on CUDA; generates up to 512 new tokens with Qwen2.5-VL architecture.
- **Custom Theme**: OrangeRedTheme with gradients for an engaging interface.
- **Queueing Support**: Handles up to 50 concurrent inferences for smooth usage.
- **Error Resilience**: Fallbacks for missing inputs; console logging for raw responses and parsed actions.

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (recommended for float16; falls back to CPU).
- Stable internet for initial model download from Hugging Face.

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/PRITHIVSAKTHIUR/Gliese-CUA-Tool-Call-8B-Demo.git
   cd Gliese-CUA-Tool-Call-8B-Demo
   ```

2. Install dependencies:
   Create a `requirements.txt` file with the following content, then run:
   ```
   pip install -r requirements.txt
   ```

   **requirements.txt content:**
   ```
   gradio==6.1.0
   transformers==4.57.1
   numpy
   torch
   torchvision
   accelerate
   qwen-vl-utils
   requests
   pillow
   spaces
   ```

3. Start the application:
   ```
   python app.py
   ```
   The demo launches at `http://localhost:7860` (or the provided URL if using Spaces).

## Usage

1. **Upload Image**: Provide a UI screenshot (e.g., PNG of a desktop or app window; height up to 500px).

2. **Enter Task**: Describe the action (e.g., "Click on the search bar" or "Type 'Hello World' in the input field").

3. **Call CUA**: Click "Call CUA" to run inference.

4. **View Results**:
   - Text: Raw model response with parsed JSON actions.
   - Image: Annotated screenshot showing action points (crosshairs with labels).

### Example Workflow
- Upload a Windows desktop image.
- Task: "Click on the start menu."
- Output: Response with `<tool_call>` block; image with red crosshair labeled "Click" on the start button.

## Troubleshooting

- **Model Loading Errors**: Verify transformers 4.57.1; check CUDA with `torch.cuda.is_available()`. Use `torch.float32` if float16 OOM occurs.
- **No Actions Parsed**: Ensure task includes actionable elements; raw output logged in console. Adjust max_new_tokens if truncated.
- **Visualization Issues**: PIL font fallback used; ensure images are RGB.
- **Queue Full**: Increase `max_size` in `demo.queue()` for higher traffic.
- **Vision Utils**: Install `qwen-vl-utils` for image processing; `process_vision_info` handles inputs.
- **UI Rendering**: Set `ssr_mode=True` if gradients fail; check CSS for custom styles.

## Contributing

Contributions encouraged! Fork the repo, create a feature branch (e.g., for multi-action support), and submit PRs with tests. Focus areas:
- Extension to multi-step workflows.
- Additional action types (e.g., scroll).
- Integration with automation libraries.
  
Repository: [https://github.com/PRITHIVSAKTHIUR/Gliese-CUA-Tool-Call-8B-Demo.git](https://github.com/PRITHIVSAKTHIUR/Gliese-CUA-Tool-Call-8B-Demo.git)

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Built by Prithiv Sakthi. Report issues via the repository.
