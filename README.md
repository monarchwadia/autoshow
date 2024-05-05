# autoshow

An example workflow for automatically creating a video transcript with show notes using ChatGPT and Whisper.

## Setup

### Install Local Dependencies

Install `yt-dlp`, `ffmpeg`, and run `npm i`.

### Mac OS

```bash
brew install yt-dlp ffmpeg
npm i
```

### Ubuntu/Debian

#### 1. Install ffmpeg

```sh
sudo apt install ffmpeg
```

#### 2. Install yt-dlp

You can download `yt-dlp` from https://github.com/yt-dlp/yt-dlp?tab=readme-ov-file . If you use the `Platform-independent zipimport binary` then you'll have to wrap the script inside a shell-executable command. To do this, you could run the following command:

```sh
# download yt-dlp and move it to /usr/local/bin/yt-dlp.py
wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp
sudo mv ./yt-dlp /usr/local/bin/yt-dlp.py
# create a script in /usr/local/bin/yt-dlp that will run yt-dlp using python
sudo sh -c 'echo "#!/usr/bin/env sh\npython /usr/local/bin/yt-dlp.py \"\$@\"" > /usr/local/bin/yt-dlp'
# make the script executable
sudo chmod 755 /usr/local/bin/yt-dlp
```

You can check if the installation worked by running `yt-dlp`

```sh
yt-dlp

# OUTPUT:
# Usage: yt-dlp.py [OPTIONS] URL [URL...]

# yt-dlp.py: error: You must provide at least one URL.
# Type yt-dlp --help to see a list of all options.
```

### Clone Whisper.cpp Repo

Run the following commands to clone `whisper.cpp` and build the `large-v2` model:

```bash
git clone https://github.com/ggerganov/whisper.cpp.git
bash ./whisper.cpp/models/download-ggml-model.sh large-v2
make -C whisper.cpp
```

## Run Autogen Bash Scripts

Run on a single YouTube video.

```bash
# short one minute video
./autogen.sh --video "https://www.youtube.com/watch?v=jKB0EltG9Jo"

# longer 30 minute video
./autogen.sh --video "https://www.youtube.com/watch?v=QhXc9rVLVUo"
```

Run on multiple YouTube videos in a playlist.

```bash
./autogen.sh --playlist "https://www.youtube.com/playlist?list=PLCVnrVv4KhXMh4DQBigyvHSRTf2CSj129"
```

Run on an arbitrary list of URLs in `urls.md`.

```bash
./autogen.sh --urls urls.md
```

## Run Autogen Node Scripts

Run on a single YouTube video.

```bash
node autogen.js video "https://www.youtube.com/watch?v=jKB0EltG9Jo"
```

Run on multiple YouTube videos in a playlist.

```bash
node autogen.js playlist "https://www.youtube.com/playlist?list=PLCVnrVv4KhXMh4DQBigyvHSRTf2CSj129"
```

Run on an arbitrary list of URLs in `urls.md`.

```bash
node autogen.js urls urls.md
```
