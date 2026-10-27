# Telegram AI Assistant

An n8n workflow that receives Telegram text messages, generates replies with OpenAI, and sends the response back to the same chat.

## Features

- Telegram message trigger and automated replies.
- OpenAI-powered AI Agent, configured with `gpt-5-mini`.
- Simple Memory keyed by Telegram chat ID for conversation context.
- Date & Time tool connected to the agent.

## Workflow

Telegram Trigger → AI Agent → Send a text message

The agent connects to an OpenAI Chat Model, Simple Memory, and a Date & Time tool.

## Setup

1. Use an n8n instance that supports the node versions in the export. Telegram webhooks require a publicly reachable HTTPS endpoint.
2. Create a Telegram bot through **@BotFather** and save its bot token in an n8n Telegram credential.
3. Add an OpenAI API credential with access to the configured model, or select another supported model.
4. Import [the workflow JSON](workflows/telegram-ai-assistant.json) into n8n.
5. Select the same Telegram credential in **Telegram Trigger** and **Send a text message**. Select your OpenAI credential in **OpenAI Chat Model**.
6. Check the workflow timezone for date/time responses.
7. Start the trigger's test listener and send a text message to your bot. Once verified, activate or publish the workflow according to your n8n version.

Credential references and instance-specific metadata have been removed from the export. Configure your own credentials after import. The workflow is exported inactive.

## Manual checks

- Send `Hello` and confirm the bot replies in the same Telegram chat.
- Say `My name is Alex`, then ask `What is my name?` in that chat to check conversation context.
- Ask for the current date and time; inspect the n8n execution to confirm whether the agent used the Date & Time tool.

## Scope and limitations

- Intended for text messages; media and voice messages are not handled.
- Memory is grouped by chat ID, so participants in a group chat share conversation context.
- Simple Memory is not a durable conversation database.
- No sender allowlist, rate limiting, or custom error handling is included.
- Telegram message length and formatting limits may require additional handling for long or formatted AI responses.
- Live execution requires your own credentials and has not been verified as part of this repository upload.

## Files

- `workflows/telegram-ai-assistant.json` — importable n8n workflow.
- `README.md` — overview, setup, and manual checks.
