# Universal Rerouter - Vercel Edition

This version is adapted to run on [Vercel](https://vercel.com) (Free Tier compatible).

## 🚀 Deployment Instructions

1.  **Install Vercel CLI** (Optional, easier to use dashboard):
    ```bash
    npm i -g vercel
    ```

2.  **Login to Vercel:**
    *   Go to [vercel.com](https://vercel.com) and sign up/login.
    *   Or use CLI: `vercel login`

3.  **Deploy:**
    *   **Option A (Web Dashboard):**
        1.  Push this `vercel_proxy` folder to a GitHub repository.
        2.  Import that repository in Vercel.
        3.  Vercel will automatically detect the Python project.
        4.  Click **Deploy**.

    *   **Option B (CLI):**
        1.  Open a terminal in this folder: `cd vercel_proxy`
        2.  Run `vercel`
        3.  Follow the prompts (Yes to everything).

## ⚙️ Configuration

Configuration is located at the top of `api/index.py`. You can edit the variables there:

*   `TARGET_UPSTREAM`: Where requests are forwarded.
*   `ENABLE_JANITORAI_PREFILL`: Enable assistant message injection.
*   `JANITORAI_PREFILL_CONTENT`: Content for assistant injection.
*   `ENABLE_JANITORAI_SYSTEM_PREFILL`: Enable system message injection.
*   `JANITORAI_SYSTEM_PREFILL_CONTENT`: Content for system injection.

## ⚠️ Important Vercel Limitations

1.  **Timeouts:** Vercel Free Tier functions have a **10-second timeout**.
    *   If the upstream API (OpenAI/etc) takes longer than 10 seconds to *start* sending a response, the request might fail.
    *   Streaming helps, but keep responses short if possible.
2.  **No Persistent Logs:** Logs are viewed in the Vercel Dashboard under the "Logs" tab of your deployment. They are not saved to files.
3.  **Cold Starts:** The first request after a while might take 2-3 seconds longer to start up.