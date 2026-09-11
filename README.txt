AliveNPCs Economy NPC Builder - Player Guide
============================================

RUN
1. Extract the whole folder anywhere (keep AliveNpcsBuilder.exe and config.json together).
2. Double-click AliveNpcsBuilder.exe.
3. On first run it auto-detects your Stardew Valley folder; if it can't, pick it manually.

AI (optional; needed for AI create/edit)
4. Open config.json in Notepad and put your own API key in "api_key"; or set the
   environment variable OPENCODEGO_API_KEY. (No key is bundled with this software.)

USING ANOTHER AI PROVIDER (optional)
- The AI features speak the standard OpenAI "chat completions" API, so you can
  use any compatible provider or a local model. Edit the "ai" block in config.json:
    * OpenAI:        api_base "https://api.openai.com/v1",     model "gpt-4o-mini"
    * DeepSeek:      api_base "https://api.deepseek.com/v1",   model "deepseek-chat"
    * OpenRouter:    api_base "https://openrouter.ai/api/v1",  model "<vendor>/<model>"
    * Groq:          api_base "https://api.groq.com/openai/v1", model "llama-3.3-70b-versatile"
    * Ollama (local): api_base "http://localhost:11434/v1",    model "llama3.1",
                      api_key "ollama" (any non-empty value)
  Put the provider's key in "api_key" (or set the env var named by "api_key_env").
- If a model rejects the request, try lowering "max_tokens" (e.g. 4096) and/or
  set "token_param" to "max_completion_tokens" (some newer models need it).
- Set "temperature": null to omit it (some models only accept the default).
- "provider" can stay "opencodego" or be any label; only "mock" is special
  (offline demo, no key or network needed).

USE
5. Select an NPC on the left to edit; click "New (AI)" and describe the character
   (what they sell/buy, personality).
6. Item fields accept Chinese or English; the tool lists candidates and you pick -
   it never guesses.
7. Click "Apply changes (save)". The tool validates -> shows the diff -> backs up -> writes.
8. Made a mistake? Click "Rollback last backup".

ITEMS OUTSIDE THE BUILT-IN LIST
- You can type a Stardew item id directly, e.g. (O)475, (W)11, (F)1234. The tool
  writes it as-is (no lookup needed).
- Or type any exact item name. If it isn't in the built-in list, the tool offers
  "Use as-is" and writes it unchanged (with a warning). The game/mod resolves it
  by name, in English or your game's language.
- Prefer strict checking? Set "allow_unverified_items": false in config.json.

UI LANGUAGE
- Set "ui_language" in config.json to a code such as "en", "zh", "ja", "es",
  "pt", "de", "fr", "ru", "ko", "it", "tr" (or a name like "English"); default
  "auto" follows the OS language.
- Only English and Chinese UI text are bundled. To add another language, drop a
  file named lang/<code>.json next to the exe (copy lang/en.json and translate
  the values). It is picked up automatically - no rebuild needed. Missing keys
  fall back to English. Community translations are welcome as pull requests.

ITEM NAMES (works in any language, no translation needed)
- The item picker/resolver can understand your language by reading the
  localized item names from YOUR OWN game files. Click "Localize item names"
  (or run `localize-items`) once. It reads
  Content/Strings/Objects.<locale>.xnb and caches the names locally.

SAFETY
- Every write is validated, previewed, and backed up first; the file is never
  changed silently.
- Fan-made tool; not affiliated with Stardew Valley or AliveNpcs Economy.
- See NOTICE.txt for third-party licenses and attribution.
