# Nethunter PulseAudio

This script allows you to start, stop, and check the status of a PulseAudio TCP stream on a specified IP address and port. It's designed to route audio over TCP/IP from a Linux environment (such as Kali NetHunter) that uses PulseAudio, making it accessible on devices connected over a network(local host in this project).

## Features

- Starts and stops a PulseAudio TCP stream on chroot like Kali Nethunter.
- Configurable IP address, port, sample rate, format, and channels.
- Includes status checks to confirm if the stream is active.

## Requirements

- **PulseAudio**: Ensure PulseAudio is installed and running on your Linux environment.
- **pactl**: Required for managing PulseAudio modules.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/IamCOD3X/Nethunter_PulseAudio.git
   cd Nethunter_PulseAudio
   ```

2. **Make the script executable**:
   ```bash
   chmod +x audio
   ```

3. **(Optional) Edit the Configuration**:
   Open the script in a text editor and adjust the configuration variables if needed:
   ```bash
   nano audio
   ```
   - `PULSE_AUDIO_IP`: IP address for the TCP stream (default is `127.0.0.1`).
   - `PULSE_AUDIO_PORT`: Port number for the TCP stream (default is `8000`).
   - `PULSE_AUDIO_RATE`: Sample rate for the audio stream (default is `48000`).
   - `PULSE_AUDIO_FORMAT`: Audio format (default is `s16le`).
   - `PULSE_AUDIO_CHANNELS`: Number of audio channels (default is `2`).

## Usage

Run the script with one of the following commands:

```bash
./audio {start|stop|status}
```

### Commands

- **start**: Starts PulseAudio (if not already running), and loads the TCP module to begin audio streaming.
- **stop**: Stops the audio stream by unloading the TCP module. If no other modules are running, PulseAudio will also be stopped.
- **status**: Checks if the audio stream is active and displays its current status.

## Example

To start the audio stream on `127.0.0.1:8000`:

```bash
./audio start
```

To stop the audio stream:

```bash
./audio stop
```

To check the stream status:

```bash
./audio status
```

## How It Works

This script uses the `pactl` command to load and unload the `module-simple-protocol-tcp` module in PulseAudio. Here’s a breakdown of each function:

- **start_pulseaudio**: Checks if PulseAudio is running, and starts it if not.
- **start_stream**: Unloads any existing instances of the module to avoid conflicts, then loads the TCP module with specified parameters.
- **stop_stream**: Unloads the TCP module and stops PulseAudio if no other modules are loaded.
- **stream_status**: Checks if the TCP module is currently loaded to confirm if the stream is active.

## Troubleshooting

- **Failed to start PulseAudio**: Ensure PulseAudio is installed and working correctly by running `pulseaudio --version`.
- **No audio stream found**: If `status` reports that no stream is found, make sure the `start` command was successful and that PulseAudio is not being blocked by firewall rules or permissions.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
