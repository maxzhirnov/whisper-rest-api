# Whisper Transcription Web Service

A simple web interface for OpenAI's Whisper speech-to-text transcription service. This application allows users to upload audio files and receive text transcriptions through a user-friendly web interface.

## Features

- Web-based UI for audio file uploads
- Support for multiple audio formats
- Real-time transcription using Whisper turbo model
- Language detection
- Simple and intuitive interface

## Launch Options

### 1. Direct Launch

#### Prerequisites
- Python 3.10 or higher
- FFmpeg
- Rust

#### Installation Steps
1. Install FFmpeg:
```bash
# Ubuntu/Debian
sudo apt-get update && sudo apt-get install ffmpeg

# MacOS
brew install ffmpeg

# Windows (using Chocolatey)
choco install ffmpeg
```

2. Install Rust:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

3. Create and activate virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # Linux/MacOS
# or
venv\Scripts\activate     # Windows
```

4. Install dependencies:
```bash
pip install -r requirements.txt
```

5. Run the application:
```bash
python app.py
```

### 2. Docker Launch

#### Prerequisites
- Docker

#### Steps
1. Build the Docker image:
```bash
docker build -t whisper-transcription .
```

2. Run the container in detached mode:
```bash
docker run -d --name whisper-api -p 5500:5500 whisper-transcription
```

#### Docker Commands Reference
```bash
# View logs
docker logs -f whisper-api

# Stop container
docker stop whisper-api

# Remove container
docker rm whisper-api

# Rebuild and restart
docker rm -f whisper-api && docker build -t whisper-transcription . && docker run -d --name whisper-api -p 5500:5500 whisper-transcription
```

## First Launch Notes

### Important: Initial Model Download

When you first start the application (either through direct launch or Docker), it will automatically download the Whisper model. Please note:

- Model size: approximately 1.5GB
- Download time: varies depending on your internet connection
- The web interface will not be accessible until the model download is complete

### How to Monitor First Launch

#### Direct Launch
- Watch the console output for download progress
- The server will start accepting connections only after model is loaded
- You'll see a message like "Running on http://0.0.0.0:5500" when ready

#### Docker Launch
- Monitor the download progress using Docker logs:
```bash
docker logs -f whisper-api
```
- The container will appear as running, but the web interface won't be accessible during model download
- Wait for the log message indicating successful model load and server start

### Expected Timeline
1. First launch initiated
2. Model download starts (~1.5GB)
3. Model loading into memory
4. Flask server starts
5. Web interface becomes accessible

### Subsequent Launches
- After the initial download, the model will be cached
- Future launches will be much faster
- Docker image rebuilds will require new model download

## Access

After launching (either method), access the web interface at:
```
http://localhost:5500
```

## Project Structure
```
whisper-web-service/
├── app.py              # Main application file
├── requirements.txt    # Python dependencies
├── Dockerfile         # Docker configuration
├── templates/         
│   └── index.html     # Web interface template
└── uploads/           # Temporary storage for uploaded files
```

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

## Troubleshooting

### Direct Launch Issues
1. **Missing dependencies**:
   - Verify FFmpeg installation: `ffmpeg -version`
   - Check Rust installation: `rustc --version`
   - Verify Python version: `python --version`

2. **Package installation errors**:
   - Update pip: `pip install --upgrade pip`
   - Install packages individually to identify issues

### Docker Issues
1. **Container not starting**:
   ```bash
   docker logs whisper-api
   ```

2. **Cannot connect to web interface**:
   - Verify container is running: `docker ps`
   - Check port mapping: `docker port whisper-api`

3. **Transcription errors**:
   - Ensure audio file format is supported
   - Check file size is under 16MB
   - Verify container has internet access for model download

## License
MIT License

Copyright (c) 2024 Maksim Zhirnov

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Contact
maximz2009@gmail.com