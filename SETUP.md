# Setup (about 5 minutes)

You need [Node.js](https://nodejs.org) 18 or newer. Nothing else. No API keys are required to run the demo.

On this machine Node lives at `C:\Program Files\nodejs` and is not on the PowerShell PATH, so the commands below add it first. On a normal install you can drop that part.

## The 3 commands to see it live

Run these in Windows PowerShell.

```powershell
# 1. Start n8n (first run downloads it, then it is cached and starts fast)
$env:Path = "C:\Program Files\nodejs;$env:Path"; $env:N8N_SECURE_COOKIE = "false"; npx n8n
```

n8n now serves the editor at http://localhost:5678 and holds this terminal open. Open a second PowerShell window for the next two commands.

```powershell
# 2. Open the editor in your browser
start http://localhost:5678

# 3. Import the workflow
$env:Path = "C:\Program Files\nodejs;$env:Path"; npx n8n import:workflow --input="C:\Users\Alvi\career\portfolio\n8n-content-pipeline\workflow.json"
```

Refresh the browser. The workflow **AI Content Pipeline - LLM Failover Demo** is now in your list. Open it and click **Execute Workflow** (bottom center). Every node on the mock path lights up green.

If this is the first time you open n8n it asks you to create an owner account. It is a local instance, so any email and password work. This demo was set up with `zal-demo@example.com`.

## Import through the UI instead

If you would rather not use the CLI: open http://localhost:5678, then use the top-right menu, choose **Import from File**, and pick `workflow.json`.

## Run it with real models (optional)

The demo runs without keys because the LLM calls are meant to fail, which is what shows the failover. To generate real articles:

1. Get a free Groq API key at https://console.groq.com.
2. Stop n8n (Ctrl+C in the first terminal), then start it again with the key in the environment:

   ```powershell
   $env:Path = "C:\Program Files\nodejs;$env:Path"
   $env:N8N_SECURE_COOKIE = "false"
   $env:GROQ_API_KEY = "your-groq-key-here"
   # optional second provider for the fallback branch:
   $env:GEMINI_API_KEY = "your-gemini-key-here"
   npx n8n
   ```

3. Execute the workflow. Now the Groq node returns a real article and the fallback branch stays idle. Pull the key to watch the run flip to Gemini.

The LLM nodes read their keys from `$env.GROQ_API_KEY` and `$env.GEMINI_API_KEY`. You can also swap those expressions for native n8n credentials if you prefer the credential manager.

## Publish to a real WordPress site (optional)

1. On the canvas, click the disabled **Publish to WordPress (real)** node and enable it.
2. Add a WordPress credential (site URL, username, application password).
3. Optionally disable the **Publish to WordPress (mock)** node so you only publish for real.

## Restart command

n8n stays installed after the first run. To bring it back up later (for screenshots, for example):

```powershell
$env:Path = "C:\Program Files\nodejs;$env:Path"; $env:N8N_SECURE_COOKIE = "false"; npx n8n
```

Then open http://localhost:5678.

## Stop it

Press Ctrl+C in the terminal running n8n. To confirm it is down:

```powershell
Get-NetTCPConnection -LocalPort 5678 -State Listen -ErrorAction SilentlyContinue
```

No output means the port is free and n8n is stopped.

## Notes

- `N8N_SECURE_COOKIE=false` lets the editor load over plain `http://localhost`. Do not use that setting on a public host.
- The mock publish target is `httpbin.org/post`, which needs outbound internet. Everything else runs locally.
