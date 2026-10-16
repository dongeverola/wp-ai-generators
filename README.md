# WordPress AI Generators

A collection of three independent WordPress plugins by Don Geverola for generating blog posts, quotes, and SEO content using the OpenAI API.

## Plugins

| Plugin | Features | Shortcode |
| --- | --- | --- |
| AI Blog Generator | Generate blog content from a topic and optional instructions; request approximately 100, 200, 300, or 400 words; save the result as a WordPress draft. | `[ai_blog_generator]` |
| AI Quote Generator | Generate text from a quote prompt. | `[ai_quote_generator]` |
| AI SEO Generator | Generate an SEO title, meta description, and keyword list for a topic. | `[ai_seo_generator]` |

Each plugin can be installed and activated separately. The quote plugin currently appears as **API Quote Generator** in the installed plugins list.

## Requirements

- A WordPress installation with permission to install plugins.
- An OpenAI API key with access to the configured model.
- A server able to make outbound HTTPS requests to `api.openai.com`.

The current code uses the OpenAI Chat Completions endpoint and the `gpt-4.1-mini` model. Other providers' API keys are not supported. API usage is associated with the configured OpenAI account; these plugins do not include API credits.

Minimum WordPress and PHP versions have not been declared or verified in this project.

## Installation

### Upload a plugin ZIP

1. Create a separate ZIP for each plugin folder, such as `ai-blog-generator.zip`.
2. Ensure the ZIP contains the plugin folder directly, with its main PHP file inside:

   ```text
   ai-blog-generator.zip
   └── ai-blog-generator/
       ├── ai-blog-generator.php
       ├── includes/
       └── templates/
   ```

3. In WordPress, open **Plugins → Add New → Upload Plugin**.
4. Upload the ZIP, install it, and activate the plugin.
5. Repeat for any other generators you want to use.

The repository's automatic GitHub source ZIP contains the collection; package the individual plugin folders separately for installation through WordPress.

### Manual installation

Copy the desired plugin folders into `wp-content/plugins/`, then activate them from **Plugins** in WordPress.

## API key setup

1. Open the corresponding settings page:
   - **Settings → AI Blog Generator**
   - **Settings → AI Quote Generator**
   - **Settings → AI SEO Generator**
2. Enter your OpenAI API key.
3. Click **Save Changes**.

Each plugin stores its own API key setting. Configure each plugin you activate. Access to these settings pages requires the WordPress `manage_options` capability.

## Usage

Add the desired shortcode to a page or post using a WordPress Shortcode block:

```text
[ai_blog_generator]
```

```text
[ai_quote_generator]
```

```text
[ai_seo_generator]
```

Open the page, enter a topic or prompt, and submit the form.

For blog generation, you can provide additional instructions and choose an approximate word count. After generation, **Save Draft** creates a draft post and provides preview and edit links.

SEO results are displayed for you to copy. The SEO plugin does not automatically update post metadata or integrate with an SEO plugin.

## Data and API keys

- Submitted topics, prompts, and additional instructions are sent to OpenAI for generation.
- API keys are stored in the WordPress options database, rather than embedded in the plugin source files.
- Settings fields visually mask saved keys, but the saved values are included in the settings page HTML and can be inspected by an administrator who can access that page.
- Keep real keys, database exports, backups, and secret configuration files out of the repository.

## Current limitations

These plugins are basic implementations and have not undergone a complete production security review.

- The shortcode forms currently have no built-in login requirement, nonce checks, or rate limiting. Making their pages public can allow visitors to consume the configured API account's usage.
- The blog draft submission currently has no explicit capability or nonce check. Restrict access to the generator page to trusted users before deployment.
- Quote output is currently rendered without HTML escaping.
- Provider and model selection are hardcoded; there is no settings interface for changing them.
- Generated content should be reviewed for accuracy and suitability before publication. Requested word counts are approximate.

## Troubleshooting

If generation fails, check that the relevant plugin's API key is saved, the account can use the configured model, and the server can reach OpenAI. The current interface provides limited error details, so a failure message alone may not identify the cause.

## Repository structure

```text
wordpress-ai-generators/
├── ai-blog-generator/
├── ai-quote-generator/
├── ai-seo-generator/
└── README.md
```

## Author

Don Geverola
