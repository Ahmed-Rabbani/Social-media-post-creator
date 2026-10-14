# Social Media Post Creator

An AI-powered social media content creation workflow built with **n8n, Google Gemini, and Pollinations AI**. This project helps users generate social media post ideas or create complete posts with AI-generated images through a custom HTML frontend.

## Features

- **AI-powered post ideas:** Generate social media content ideas from a simple text prompt.
- **Complete post creation:** Generate a title, description, image prompt, tags, hashtags, call to action, alt text, and slug.
- **AI image generation:** Generate images using Pollinations AI with the Flux model.
- **Custom frontend:** Send a text prompt from the frontend to the n8n webhook and display the response.
- **Automated workflow:** Connect AI services through n8n instead of manually performing each step.
- **Local deployment:** Run the workflow locally using your own n8n instance.
- **Two working modes:** Both modes have been tested successfully.

## Tech Stack

| Technology | Purpose |
|---|---|
| n8n 2.41.6 | Workflow automation and webhook handling |
| Google Gemini Flash Lite | AI-powered text and content generation |
| Pollinations AI | AI image generation |
| HTML, CSS, JavaScript | Custom frontend interface |

## How It Works

1. The user enters a text prompt in the frontend.
2. The frontend sends the request to the n8n webhook.
3. The workflow processes the prompt using Google Gemini.
4. For image generation, the workflow sends the image prompt to Pollinations AI.
5. The workflow returns its generated content and image result to the frontend.

The exact output depends on the selected mode and the input prompt.

## Requirements

Before starting, make sure you have:

- A computer running Windows, macOS, or Linux.
- A working n8n instance. This project was tested with n8n **2.41.6**.
- A Google Gemini API key.
- A Pollinations AI API key.
- The workflow JSON file from this repository.
- The frontend HTML file: `Soical Media Post Crearot frontend.html`.
- An internet connection for the external AI services.

> **Important:** The workflow runs locally, but Gemini and Pollinations AI are external services. Internet access and valid credentials are required to use them.

## Installation and Setup

### 1. Clone or Download the Repository

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/Social-media-post-creator.git
cd Social-media-post-creator
```

Replace `YOUR-USERNAME` with your GitHub username.

Alternatively, download the repository as a ZIP file from GitHub and extract it.

### 2. Open n8n

Start your local n8n instance and open it in your browser.

For a typical local installation:

```text
http://localhost:5678
```

If your n8n instance uses a different address or port, use your own URL.

### 3. Import the Workflow

1. Open n8n.
2. Create a new workflow or open the workflow editor.
3. Open the workflow menu and choose the import option.
4. Select the sanitized workflow JSON file included in the repository.
5. Save the imported workflow.

The exported workflow does not include your private credentials. You must configure them before running the workflow.

### 4. Configure Google Gemini Credentials

Google Gemini is used to generate social media content.

1. Open [Google AI Studio](https://aistudio.google.com/apikey).
2. Sign in with your Google account.
3. Create an API key, following Google's available account and API requirements.
4. Copy the key and keep it private.
5. In n8n, open the Google Gemini node.
6. Open the credentials selector and create or select the appropriate Google Gemini API credential.
7. Enter your API key in the credential setup.
8. Save the credential and select it in the relevant node.
9. Repeat for other Gemini nodes if the workflow requires separate credential assignments.

Do not paste your Gemini API key into this README or commit it to GitHub.

### 5. Configure Pollinations AI for Image Generation

This workflow uses Pollinations AI for image generation. The imported workflow contains a placeholder for the authorization key, so you must replace it with a valid key.

#### Step 1: Open Pollinations AI

Visit:

https://enter.pollinations.ai

Sign in or create an account and follow the current instructions for obtaining an API key.

#### Step 2: Create an API Key

1. Open the API key or account settings available on the Pollinations website.
2. Create a key suitable for server-side use.
3. Copy the key securely.

For an n8n workflow, a server-side secret key is generally the appropriate choice. Follow Pollinations' current account and authorization requirements.

Official documentation: https://gen.pollinations.ai/docs

#### Step 3: Open the Image Generation Node

1. Return to n8n.
2. Open the HTTP Request node responsible for Pollinations image generation.
3. Locate the request's authorization header.
4. Find the placeholder value:

```text
Bearer YOUR_POLLINATIONS_API_KEY_HERE
```

5. Replace the placeholder with your actual key, keeping the `Bearer ` prefix.

The resulting value should follow this format:

```text
Bearer YOUR_ACTUAL_API_KEY
```

Do not use the example text as a real key.

#### Step 4: Save and Test

1. Save the node configuration.
2. Run a test execution.
3. Check whether the image-generation request succeeds.
4. If it fails, check the key, authorization header, model availability, and current account usage limits.

**Security warning:** Keep secret API keys inside n8n's server-side credentials or protected node configuration. Never publish them in your HTML frontend, README, screenshots, or public workflow JSON.

#### Is Pollinations AI Free?

Pollinations may provide access subject to its current account, usage, and quota rules. A working API key does not guarantee unlimited free image generation. Check the current terms, balance, and limits before using the workflow extensively.

### 6. Connect the Frontend to n8n

The frontend sends a simple text prompt to the n8n webhook.

1. Open the imported workflow.
2. Select the Webhook node.
3. Check its HTTP method and use the configured `POST` method.
4. Copy the **Test URL** shown in the node.
5. Open `Soical Media Post Crearot frontend.html` in your code editor.
6. Locate the webhook URL configuration in the frontend code.
7. Replace the existing URL or placeholder with your n8n Test URL.
8. Save the HTML file.

If the frontend does not contain a configurable webhook URL yet, add the URL to its request configuration before using it.

### 7. Test the Workflow

1. Open the workflow in n8n.
2. Click **Listen for Test Event** or the equivalent test-execution control.
3. Open the frontend in your browser.
4. Enter a text prompt.
5. Submit it.
6. Wait for the workflow to execute.
7. Check the n8n execution details if the frontend does not display a response.

Use the Test URL while developing. n8n's test webhook is intended for testing and is available only while the test listener is active.

### 8. Use the Production Webhook

After testing:

1. Save the workflow.
2. Make sure all credentials and API keys are configured.
3. Publish or activate the workflow using the option available in your n8n version.
4. Open the Webhook node.
5. Copy the **Production URL**.
6. Update the webhook URL in your frontend.
7. Test the frontend again.

A production webhook is used when the workflow is published. Execution details can be inspected from n8n's Executions view.

For more information, read the [official n8n Webhook documentation](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/).

## Using the Frontend

1. Open the HTML frontend in your browser.
2. Enter a topic or a description of the content you want.
3. Submit the prompt.
4. Wait for n8n to process the request.
5. Review the returned result.

Example prompts:

```text
Generate social media post ideas for a technology brand.
```

```text
Create a social media post promoting a new wireless earbuds product.
```

```text
Create engaging content for a fitness brand's Instagram page.
```

The generated content depends on the prompt and the selected workflow mode.

## Troubleshooting

### Image Generation Fails

- Verify that the Pollinations API key is valid.
- Confirm that the authorization header contains the `Bearer ` prefix.
- Check that the placeholder has been replaced.
- Check the current API usage limits and model availability.
- Inspect the HTTP Request node's error details.

### Gemini Content Generation Fails

- Verify that the Gemini API key is valid.
- Check that the correct n8n credential is selected.
- Review the node's execution output for authentication, quota, or request errors.

### Frontend Does Not Receive a Response

- Check the webhook URL configured in the HTML file.
- Confirm that the workflow is listening for a test request or published for production use.
- Inspect the n8n execution for errors.
- Confirm that the workflow is configured to return the expected response.

### Test Webhook Does Not Work

- Use the Test URL, not the Production URL, during testing.
- Start the test listener before submitting the frontend request.
- If using the Production URL, make sure the workflow is published.

### Frontend Cannot Connect to Local n8n

- Confirm that n8n is running.
- Verify the hostname and port.
- Check browser console errors and any CORS-related issues if the request is blocked.

## Security

- Never commit real API keys or credentials.
- Do not expose a server-side Pollinations secret key in frontend JavaScript.
- Keep private configuration out of screenshots and public examples.
- Use a `.gitignore` file for local secrets and other files that should not be committed.
- Remember that `.gitignore` does not remove a secret that has already been committed. Revoke and replace any exposed key.
- Do not expose a publicly accessible webhook without considering authentication and abuse prevention.

## Project Structure

The repository contains the workflow export and the custom frontend.

```text
Social-media-post-creator/
├── README.md
├── Social media Creator - credentials removed.json
└── Soical Media Post Crearot frontend.html
```

If your actual filenames differ, update the names in this section to match the repository.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

If you publish this repository under MIT, include a `LICENSE` file containing the standard MIT License text and your copyright details.

## Credits

- [n8n](https://n8n.io/) — workflow automation
- [Google AI Studio](https://aistudio.google.com/) — Gemini API access
- [Pollinations AI](https://pollinations.ai/) — AI image generation

---

**Note:** This is a portfolio and automation project. API availability, model names, account requirements, and usage limits can change. Check the official service documentation when configuring the workflow.
