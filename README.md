# Stakeholder Reaction Simulator; Direction to replicate:

Pre-test crisis statements against a simulated stakeholder panel. The page is a single `index.html`. A small Cloudflare Worker (`worker.js`) lets visitors run live simulations on your OpenAI key without the key ever appearing in the page.

> Never put an API key in `index.html`. Anything in a public repo or GitHub Pages site can be read by anyone, and OpenAI automatically revokes keys it finds on GitHub.

## 1. Publish the page (GitHub Pages)

1. Create a public repository and upload `index.html`.
2. Go to **Settings > Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
3. Your site will be at `https://<your-username>.github.io/<repo-name>/`.

At this point the page works in sample mode, and visitors can use their own keys.

## 2. Deploy the proxy (Cloudflare Workers, free tier)

1. Sign in at dash.cloudflare.com and open **Workers & Pages > Create > Create Worker**.
2. Name it (for example `reaction-proxy`), click **Deploy**, then **Edit code**. Replace everything with the contents of `worker.js` and deploy again.
3. Open the Worker's **Settings > Variables and Secrets** and add:

| Name | Type | Value |
|---|---|---|
| `OPENAI_API_KEY` | Secret | your OpenAI key |
| `ALLOWED_ORIGINS` | Text | `https://<your-username>.github.io` |
| `ALLOWED_MODELS` | Text | `gpt-4.1-mini` (optional; first is the default) |
| `ACCESS_CODE` | Secret | optional; a code you share with people you invite |
| `MAX_PER_MINUTE` | Text | optional; default `30` |

4. Copy the Worker URL, for example `https://reaction-proxy.<you>.workers.dev`.

## 3. Connect the page to the proxy

At the top of the script in `index.html`, set:

```js
const CONFIG = {
  proxyUrl: "https://reaction-proxy.<you>.workers.dev",
  requireCode: false,      // true if you set ACCESS_CODE
  proxyModel: "gpt-4.1-mini" // must be in ALLOWED_MODELS
};
```

Commit the change. Visitors will now see **Live, on the site owner's key** as the default connection.

## 4. Protect your spending

- In the OpenAI dashboard, put this key in its own project and set a monthly **budget limit**.
- Set an `ACCESS_CODE` if you only want invited people (for example, an interviewer) to use your key.
- The Worker fixes the simulation instructions on the server, caps request size, limits requests per visitor, and only allows the models you list, so the proxy cannot be used as a general chatbot.
- The origin check stops other websites from using your proxy, but it does not stop someone calling it directly. The access code and budget limit are what protect you there.

## Notes

- A run makes one scoring call per persona, draft and run, one head-to-head call per persona and run, and one fact check and one consolidation call per draft. Five personas, two drafts and two runs make 34 calls. The page shows the count before you run.
- The default model, gpt-4.1-mini, accepts temperature, so repeat runs vary. GPT-5 family models ignore temperature.
- The page shows which endpoint answered and which model replied, so you can always confirm your key was used.
- Simulated reactions are advisory. Use fictional or approved, non-confidential material only.
