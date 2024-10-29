# Whisper Transcription Web Service

A simple web interface for OpenAI's Whisper speech-to-text transcription service. This application allows users to upload audio files and receive text transcriptions through a user-friendly web interface.

## Features

- Web-based UI for audio file uploads
- Support for multiple audio formats
- Real-time transcription using Whisper turbo model
- Language detection
- Simple and intuitive interface

## Prerequisites

Before running this project, make sure you have the following installed:

- Python 3.9 or higher
- FFmpeg
- Rust

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd whisper-web-service
```

2. Install FFmpeg:
```bash
# Ubuntu/Debian
sudo apt-get update && sudo apt-get install ffmpeg

# MacOS
brew install ffmpeg

# Windows (using Chocolatey)
choco install ffmpeg
```

3. Install Rust:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

4. Install Python dependencies:
```bash
pip install -r requirements.txt
```

## Project Structure
```
whisper-web-service/
├── app.py              # Main application file
├── requirements.txt    # Python dependencies
├── templates/         
│   └── index.html     # Web interface template
└── uploads/           # Temporary storage for uploaded files
```

## Usage

1. Start the application:
```bash
python app.py
```

2. Open your web browser and navigate to:
```
http://localhost:5500
```

3. Upload an audio file and click "Transcribe" to get the text transcription.

## Supported Audio Formats

- MP3
- WAV
- M4A
- And other formats supported by FFmpeg

## Technical Details

- Built with Flask web framework
- Uses OpenAI's Whisper turbo model for transcription
- Implements temporary file storage for processing
- Includes error handling and loading states
- Responsive web design

## Limitations

- Maximum file size: 16MB
- Processing time depends on file size and system capabilities
- Requires active internet connection for initial model download

## Development

To contribute to this project:

1. Fork the repository
2. Create a new branch for your feature
3. Make your changes
4. Submit a pull request

## Troubleshooting

Common issues and solutions:

1. **FFmpeg not found**
   - Ensure FFmpeg is properly installed and accessible in your system PATH

2. **Model download issues**
   - Check your internet connection
   - Ensure enough disk space for model storage

3. **File upload errors**
   - Verify file size is under 16MB
   - Check file format compatibility

## Security Notes

- Implements basic file validation
- Uses secure filename handling
- Temporary file cleanup after processing

## Acknowledgments

- OpenAI for the Whisper model
- Flask framework contributors
- FFmpeg project# whisper-rest-api
