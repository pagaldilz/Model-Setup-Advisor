# LM Studio + Ollama Model Setup Advisor

A single-page web application that helps you optimize your local AI model setup by scanning your LM Studio and Ollama model folders, detecting model sizes, and providing automatic GPU/CPU split suggestions.

## Features

- **Local Scanning**: Recursively scans your LM Studio and Ollama model directories for `.gguf` files
- **Hardware-Aware Suggestions**: Calculates optimal GPU layer offloading based on your VRAM capacity
- **Model Analysis**: Extracts quantization information and estimates model layers from filenames
- **Sortable Tables**: Click on any column header to sort the model list (ascending/descending)
- **Privacy Focused**: All scanning happens locally in your browser - no data is uploaded to any server
- **Cross-Platform**: Works with both LM Studio and Ollama model formats

## How It Works

1. **Hardware Detection**: Enter your GPU VRAM and system RAM specifications
2. **Folder Selection**: Choose your LM Studio and Ollama model directories
3. **Automatic Scanning**: The app recursively scans for `.gguf` files in selected directories
4. **Layer Estimation**: Estimates total model layers based on model name patterns (7B, 13B, etc.)
5. **GPU Optimization**: Calculates suggested GPU layers to use ~80% of your VRAM
6. **Visual Feedback**: 
   - Green indicators for models that fit entirely in VRAM
   - Yellow indicators for models requiring partial GPU offloading
## Sorting Functionality

The model table now supports sorting by any column:
- **Model Name**: Sort alphabetically by model file name
- **Source**: Group LM Studio and Ollama models
- **Quantization**: Sort by quantization type (e.g., Q4, Q5, Q8)
- **Size**: Sort by file size (numerical order)
- **Est. Layers**: Sort by estimated model layers
- **Suggested GPU Layers**: Sort by recommended GPU layer count

To use sorting:
1. Click on any column header to sort in ascending order (↑ indicator appears)
2. Click the same header again to sort in descending order (↓ indicator appears)
3. Click a different header to sort by that column instead

## Usage Instructions

1. Open `lm_studio_ollama_model_setup_advisor_single_page_html.html` in a supported browser
2. Enter your hardware specifications:
   - GPU VRAM (GB)
   - System RAM (GB)
3. Select your model directories:
   - For LM Studio: Select the models folder (usually `~/LM Studio/models`)
   - For Ollama: Select the parent folder of `blobs` (usually `~/.ollama`)
4. Click "Rescan All Folders" to refresh results after changing folders or hardware specs
5. Review the suggested GPU layer allocations for each model

## Technical Implementation

### Core Functions

- `estimateLayers()`: Estimates total model layers based on model name patterns
- `scanDirectory()`: Recursively scans directories for `.gguf` files using the File System Access API
- `recompute()`: Calculates GPU layer suggestions based on VRAM budget (80% of specified VRAM)
- `parseQuant()`: Extracts quantization information from filenames

### Technologies Used

- Vanilla JavaScript (no frameworks)
- HTML5 File System Access API
- CSS3 with modern styling techniques
- Responsive grid layout

### Browser Compatibility

This application requires the File System Access API which is available in:
- Chrome 86+
- Edge 86+
- Other Chromium-based browsers with similar API support

**Note**: Firefox and Safari do not currently support the File System Access API required for directory scanning.

## Privacy & Security

- **Zero Data Collection**: No data leaves your device
- **Local Processing**: All file scanning and calculations happen locally in your browser
- **No Server Communication**: The application works completely offline after loading
- **Temporary Access**: Directory permissions are only valid for the current browser session

## Ollama Specific Notes

Ollama stores models in a `blobs/` directory. When selecting your Ollama models folder, choose the **parent folder** of `blobs` (typically `~/.ollama` on most systems).

## File Structure

```
lm_studio_ollama_model_setup_advisor_single_page_html.html
```

This is a single-file application with no external dependencies.

## Contributing

This is a self-contained single-file application. To contribute:

1. Fork the repository
2. Make your changes to the HTML file
3. Test in supported browsers
4. Submit a pull request

## License

This project is open source and available under the MIT License.