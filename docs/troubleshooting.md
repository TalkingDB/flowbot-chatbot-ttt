# Troubleshooting

[Docs home](README.md) › Troubleshooting

| Symptom | Likely cause | Fix |
| :--- | :--- | :--- |
| The bot always says "Please upload a document to train" | Flowbot sent no graph IDs for this user or chat | Upload a document through the chat and wait until TTT finishes indexing it |
| The bot says "Sorry, I don't have an answer for that." for every question | The TTT request failed or returned no elements; the error is logged as "TTT request failed" | Check `TTT_URL` points at `/v1/queries`, and that Flowbot's `NEXT_PUBLIC_TDB_TTT_SERVICE_AUTHORIZATION` holds a valid TTT API key |
| TTT returns 401 | The authorization header from Flowbot is missing or wrong | Create a key on the TTT service (`POST /auth/api-keys`) and set it in Flowbot |
| The model call fails with 401 | `GPT_BEARER_TOKEN` is missing or invalid | Set it in `server/.env` |
| `.env` values are not picked up | The folder inside Flowbot is not named `flowbot-chatbot-ttt`, so `configuration/flowbot-chatbot-ttt/server/.env` does not exist | Keep the folder name, or change the path in `server/index.js` |
| The answer says the documents do not cover the question, but they do | TTT returned other passages in its top 5 | Rephrase with words from the document; check what TTT returns for the same question with a direct `POST /v1/queries` |
| Words appear all at once instead of streaming | A proxy is buffering the event stream | Turn off buffering for Flowbot's `/api/chat` |

---

**Related:** [Architecture](architecture.md) · [README](../README.md)
