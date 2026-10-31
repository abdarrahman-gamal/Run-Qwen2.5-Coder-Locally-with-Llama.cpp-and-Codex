# Run-Qwen2.5-Coder-Locally-with-Llama.cpp-and-Codex
Run Qwen2.5-Coder Locally with Llama.cpp and Codex
# Setup Steps

Download from [https://llama.app/](https://llama.app/)

In PowerShell do:

```powershell
llama serve -hf Qwen/Qwen2.5-Coder-3B-Instruct-GGUF:Q6_K `
  --alias qwen2.5-coder `
  --jinja `
  -c 30720 `
  -ngl all `
  --cache-type-k q8_0 `
  --cache-type-v q8_0 `
  -fa on `
  --port 9931
```

Keep working (if need to close look down).

Download ChatGPT Codex.

In `user\.codex\config.toml`:

First of file >

```toml
model = "qwen2.5-coder"
model_provider = "llamacpp"
```

End of file >

```toml
[model_providers.llamacpp]
name = "Local Llama"
base_url = "http://127.0.0.1:9931/v1"
wire_api = "responses"
requires_openai_auth = false
```

For the error:

1. **Error submitting message**  
   **Work browser access requires an authenticated account**

### How to Fix It (In 2 Clicks)

#### 1. Click the button on your screen

Click the white button inside the black banner [cite: 1.3.2]:  
👉 **Continue without administrator access**

This instructs Codex to run in standard ("unelevated") (look down) mode, which operates without administrative permissions[[3](https://www.google.com/url?sa=E\&q=https%3A%2F%2Fvertexaisearch.cloud.google.com%2Fgrounding-api-redirect%2FAUZIYQE8BnUFYffs26CA2SgAAzq72N9dAo1xb0Ur3boraCLsZB_486UDa--6N57hqo6pVZEtBh3ymSVw-MNPM_5N8znz8Z4-bFIQiISMl5nnI_tPJfoh-QlLI5jWJn51rSMVQ8Ht)].

#### 2. Start a New Chat

Click the **+ New chat** button at the top-left corner.  
*(The failed heloow chat has a red error icon (!) because its session was aborted; it cannot be reused [cite: 1.2.8]).*

Now send a new message in the fresh chat window [cite: 1.3.2].

(No slides, spreadsheets, and web research.)

---

## 1. Stop the current server

In the CMD window running `llama serve`, press Ctrl+C.

Then open a new CMD window and run:

```cmd
netstat -ano | findstr :9931
```

If a process is listening on port `9931`, the last column is its PID (process ID). Check which program owns it:

```cmd
tasklist /FI "PID eq 1234"
```

Replace `1234` with the actual PID. If it is an old `llama.exe` process, stop that specific process:

```cmd
taskkill /PID 1234 /F
```

Do not terminate a PID until you've confirmed which program it belongs to.

---

### The Two Modes Compared

| Feature | Default Mode (Elevated Sandbox) | Unelevated Mode |
| --- | --- | --- |
| **How it runs** | Tries to create a dedicated guest Windows account (e.g. CodexSandbox) and custom firewall rules. | Runs as **you** (`C:\Users\gaa77`), using standard user permissions. |
| **Admin rights** | **Required.** Fails if you decline UAC or lack administrator rights. | **None needed.** Starts instantly. |
| **Access to dev tools** | Often **breaks** because the separate sandbox user cannot see your PATH, Python, Node, or Git configs. | **Perfect.** Automatically accesses your installed compilers, Python venvs, and Git credentials. |
| **Isolation level** | Virtualized OS-level user jail. | Standard user-space process. |

### What You Need to Know About Safety

Because unelevated runs commands with the same permissions as your Windows login:

- Any script the model executes can read and modify files in your user folder.
- **Built-in Protection:** Notice the **Ask for approval** toggle (the hand icon ✋) at the bottom left of your composer. Keep this enabled so Codex prompts for confirmation before running terminal commands or modifying files.


### HauhauCS/Qwen3.5-2B-Uncensored-HauhauCS-Aggressive:Q6_K

```
llama serve -hf HauhauCS/Qwen3.5-2B-Uncensored-HauhauCS-Aggressive:Q6_K `
    --alias qwen3.5-2b-uncensored `
    --jinja `
    --no-mmproj `
    -c 32768 `
    --cache-type-k q8_0 `
    --cache-type-v q8_0 `
    -fa on `
    --port 9931
```
