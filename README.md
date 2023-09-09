# LLaMA 2 Chatbot App ⚡

This is an experimental Streamlit chatbot app built for LLaMA2 (or any other LLM). The app provides an option to select multiple LLaMA2 API endpoints on Replicate.

![demo](demos/Llama%20Chatbot.gif)

## Features

- Option to select between different LLaMA2 chat API endpoints (7B, 13B or 70B). The default is 70B.
- Configure model hyperparameters from the sidebar (Temperature, Top P, Max Sequence Length).
- Includes "User:" and "Assistant:" prompts for the chat conversation.
- Each model (7B, 13B & 70B) runs on Replicate - (7B and 13B run on one A100 40Gb, and 70B runs on one A100 80Gb).

## Installation

- Clone the repository
- [Optional] Create a virtual python environment with the command `python -m venv .venv` and activate it with `source .venv/bin/activate`
- Install dependencies with `pip install -r requirements.txt`
- Create an account on [Replicate](https://replicate.com/)
- Make your own `.env` file with the command `cp .env_template .env`. Then edit the `.env` file and add your:
    - [Replicate API token](https://replicate.com/account) as `REPLICATE_API_TOKEN`
- Run the app with `streamlit run llama2_chatbot.py`
- Dockerfile included to [deploy this app](#deploying-on-flyio) in Fly.io

(Note: if you are using a Mac, you may need to use the command `python3` instead of `python` and `pip3` instead of `pip`)

## Usage

- Start the chatbot by selecting an API endpoint from the sidebar.
- Configure model hyperparameters from the sidebar.
- Type your question in the input field at the bottom of the app and press enter.

## Deploying on fly.io
1. First you should [install flyctl](https://fly.io/docs/hands-on/install-flyctl/) and login from command line
2. `fly launch` -> this will generate a fly.toml for you automatically
3. `fly deploy --dockerfile Dockerfile` --> this will automatically package up the repo and deploy it on fly. If you have a free account, you can use `--ha=false` flag to only spin up one instance
4. Go to your deployed fly app dashboard, click on `Secrets` from the left hand side nav, and click on `Use the Web CLI to manage your secrets without leaving your browser`. Once you are on your app's web CLI, export all secrets needed. i.e `export REPLICATE_API_TOKEN=your_replicate_token`. Refer to .env.example file for necessary secrets. 
