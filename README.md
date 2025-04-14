# Viral Self-Improvement Content Generator

This project uses Google's Gemini API to generate viral-worthy motivational self-improvement scripts with accompanying inspirational images and audio narration using Kokoro TTS.

## Project Structure

```
├── main.py                 # Main application entry point
├── requirements.txt        # Project dependencies
├── src/                    # Source code package
│   ├── generators/         # Content generation modules
│   │   ├── script_generator.py   # Creates viral self-improvement scripts
│   │   ├── image_generator.py    # Generates images from prompts
│   │   └── audio_generator.py    # Converts scripts to speech using Kokoro TTS
│   └── utils/              # Utility modules
│       ├── config.py       # Configuration utilities
│       ├── topic_data.py   # Database of 200+ self-improvement topics
│       └── media_utils.py  # Media processing utilities
├── data/                   # Data storage directory
└── output/                 # Output storage directories
    ├── scripts/            # Generated motivational scripts
    ├── images/             # Generated images (YouTube 16:9 format)
    └── audio/              # Generated audio narrations
```

## Setup

1. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

2. Run the application:
   ```
   python main.py
   ```

   Additional command line options:
   ```
   python main.py --auto             # Run in automatic mode
   python main.py --list-voices      # Display available TTS voices
   python main.py --voice af_bella   # Specify a TTS voice
   python main.py --skip-audio       # Skip audio generation
   ```

   Note: API keys are already configured in `src/utils/config.py`

## Development

This project follows standard Python package structure for better organization:

- **src/** - Contains all source code in a proper Python package structure
- **data/** - Reserved for any data files needed by the application
- **output/** - Organized storage for generated content

## How It Works

1. Select from 200+ self-improvement topics or let the system choose one randomly
2. The script generator creates viral, highly shareable motivational content with image prompts using Gemini's text generation capabilities
3. The image generator takes those prompts and creates visual representations in YouTube 16:9 format using Gemini's image generation model
4. The audio generator converts the script into natural-sounding speech using Kokoro TTS
5. All outputs are saved with timestamps for easy tracking

## Output

- Motivational scripts are saved as markdown files in the `output/scripts` directory
- YouTube-optimized images (16:9 aspect ratio) are saved in the `output/images` directory
- Audio narrations are saved as WAV files in the `output/audio` directory
- All outputs use matching timestamps for easy correlation

## Models Used

- Text Generation: `gemini-2.0-flash-thinking-exp-01-21` (Google Gemini)
- Image Generation: `gemini-2.0-flash-exp-image-generation` (Google Gemini)
- Audio Generation: `Kokoro-82M` (Kokoro TTS)

## Note

API keys are already configured in the code, so you can run the application immediately without additional setup.

## Run on Google Colab

You can run this project directly in Google Colab without any local setup. Just copy and paste this code cell:

```python
# Clone the repository
!git clone https://github.com/motivationai/motivation-ai-.git
%cd motivation-ai-

# Install required packages
!pip install -q google-generativeai requests pillow

# Create necessary directories
!mkdir -p output/scripts output/images

# Run the application in automatic mode with audio generation
!python main.py --auto --voice af_bella

# Display generated images (if any)
import glob
from IPython.display import Image, display, Markdown

# Display the generated script
script_files = sorted(glob.glob('output/scripts/*.md'))
if script_files:
    with open(script_files[-1], 'r') as f:
        script_content = f.read()
    display(Markdown(script_content))

# Display any generated images
image_files = sorted(glob.glob('output/images/*.*'))
for img_file in image_files:
    if not img_file.endswith('.gitkeep'):
        display(Image(img_file))
        print(f"Image: {img_file}")
```

This code will:
1. Clone the repository
2. Install dependencies
3. Run the application
4. Display the generated script and images directly in the notebook
