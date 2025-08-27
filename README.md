
<div align="center">
  <img src="https://raw.githubusercontent.com/videosdk-community/ai-agent-examples/main/.github/banner.png" alt="VideoSDK AI Agents Banner" style="width:100%;">
<a href="https://docs.videosdk.live/ai_agents/introduction" target="_blank"><img src="https://img.shields.io/badge/_Documentation-4285F4?style=for-the-badge" alt="Documentation"></a>
<a href="https://www.youtube.com/playlist?list=PLrujdOR6BS_1fMqsHd9tynAg0foSRX5ti" target="_blank"><img src="https://img.shields.io/badge/_Tutorials-FF0000?style=for-the-badge&logo=youtube&logoColor=white" alt="Video Tutorials"></a>
<a href="https://dub.sh/o59dJJB" target="_blank"><img src="https://img.shields.io/badge/_Get_Started-4285F4?style=for-the-badge" alt="Get Started"></a>
<a href="https://discord.gg/7vKnd7azNT" target="_blank"><img src="https://img.shields.io/badge/_Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord Community"></a>
<a href="https://pypi.org/project/videosdk-agents/" target="_blank"><img src="https://img.shields.io/badge/_pip_install-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="PyPI Package"></a>
</div>

# Ai Voice Agent For Call Center



This repository contains ai voice agent for call center, built using the VideoSDK Agents architecture with a [cascading pipeline](https://docs.videosdk.live/ai_agents/core-components/cascading-pipeline).

## Description

This Agent is designed to act as a helpful assistant as ai voice agent for call center. It can answer questions and perform tasks related to this domain.

## Features

- **Cascading Pipeline:** Uses a Speech-to-Text (STT), Large Language Model (LLM), and Text-to-Speech (TTS) pipeline.
- **Real-time Interaction:** Provides a conversational experience.
- **Customizable:** The agent's instructions can be easily modified in `main.py`.

## Getting Started

### Prerequisites

- Python 3.12 or higher
- A VideoSDK Authentication [Token](https://app.videosdk.live?utm_source=ai-voice-agent-for-call-center&utm_medium=github-repo-auto&utm_campaign=github-repo-auto)
- API keys for [Deepgram](https://console.deepgram.com), [OpenAI](https://platform.openai.com/api-keys), and [ElevenLabs](https://elevenlabs.io/app/developers/api-keys)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/videosdk-community/ai-voice-agent-for-call-center.git
   ```

2. **Navigate to the project directory:**
   ```bash
   cd ai-voice-agent-for-call-center
   ```

3. **Create and activate a virtual environment:**
   ```bash
   python3.12 -m venv venv
   source venv/bin/activate
   ```

4. **Install the dependencies:**

   You can install the dependencies using the `requirements.txt` file:
   ```bash
   pip install -r requirements.txt
   ```
   Alternatively, you can install the packages directly:
   ```bash
   pip install "videosdk-agents[deepgram,openai,elevenlabs,silero,turn_detector]"
   ```

### Configuration

1. **Create a `.env` file** in the root of the project.

2. **Add your API keys and tokens** to the `.env` file:
   ```
   DEEPGRAM_API_KEY=<Your Deepgram API Key>
   OPENAI_API_KEY=<Your OpenAI API Key>
   ELEVENLABS_API_KEY=<Your ElevenLabs API Key>
   VIDEOSDK_AUTH_TOKEN=<VideoSDK Auth token>
   ```

### Running the Agent

```bash
python main.py
```

## How It Works

The agent uses a cascading pipeline:
1. **DeepgramSTT:** Transcribes the user's speech to text.
2. **OpenAILLM:** Generates a response based on the transcribed text and the agent's instructions.
3. **ElevenLabsTTS:** Converts the LLM's text response into speech.

This entire process is orchestrated by the VideoSDK Agents framework.

## Code Explanation

The `main.py` file contains the complete logic for the AI Voice Agent.

- **`MyVoiceAgent` class:** This class inherits from the base `Agent` class provided by the VideoSDK.
    - `__init__`: The agent's instructions, are passed to the `super().__init__`. These instructions define the agent's persona and purpose.
    - `on_enter` and `on_exit`: These are event handlers that are triggered when the agent joins or leaves a session. They use `self.session.say()` to have the agent speak.

- **`start_session` function:** This is the main asynchronous function that sets up and runs the agent.
    - It initializes `MyVoiceAgent`.
    - It creates a `CascadingPipeline`, which is the core of the agent's functionality. This pipeline connects the STT, LLM, and TTS services.
    - An `AgentSession` is created to manage the agent's connection and interaction.
    - `context.connect()` and `session.start()` connect the agent to a room and start the session.

- **`make_context` function:** This function prepares the `JobContext`, which includes `RoomOptions`. The `playground=True` setting allows you to easily test the agent in a VideoSDK playground environment.

- **`if __name__ == "__main__":`:** This block starts the agent by creating and running a `WorkerJob`.

## License

This project is licensed under the MIT License.
