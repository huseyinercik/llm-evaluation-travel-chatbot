# Copilot Agent Instructions

## Promptfoo Test Organization

- Keep every Promptfoo test suite under `travel-chatbot/`. Do not add test-suite folders at the repository root.
- Put each non-deterministic assertion type in its own folder under `travel-chatbot/`, named for the assertion type (for example, `travel-chatbot/factuality/`).
- Each assertion-type folder must contain:
  - `<assertion-type>config.yaml`, containing the Promptfoo configuration and that assertion's grading options.
  - `input.yaml`, containing the test cases for that assertion type.
  - `providers.yaml`, containing the chatbot provider configuration.
- Reference the local files from the config with `file://providers.yaml` and `file://input.yaml`.
- Keep assertion types separate unless a user explicitly requests a combined evaluation. For a requested combined evaluation, create a dedicated folder named for the included assertion types and keep each assertion as a separate assertion entry in the config.

## Environment Variables and Providers

- Read credentials and endpoint values from the repository-root `.env` file. Never hardcode secrets, tokens, or environment-specific endpoint values in YAML.
- Keep `.env` out of version control. Update `.env.example` with placeholder variable names when a new environment variable is required; never put real credentials there.
- Use `{{env.VARIABLE_NAME}}` for environment-backed provider settings and configure OpenAI providers to read `OPENAI_API_KEY` through `apiKeyEnvar`.
- `providers: file://providers.yaml` selects the chatbot under test; it is not the assertion grader. Whenever an assertion uses an embedding provider, configure it explicitly as `openai:embeddings:text-embedding-3-small`, even when the chatbot provider is referenced through `file://providers.yaml`. Do not substitute another embedding provider.
- Keep assertion-specific LLM graders, such as `llm-rubric`, configured with their required LLM provider; the embedding-provider rule applies when the assertion uses embeddings.
- For the travel chatbot HTTP provider, read its endpoint and bearer token from the existing `HF_Endpoint` and `HF_TOKEN` environment variables.

## Naming and Scope

- Use `input.yaml` consistently, even if an existing suite uses a different filename; update its config reference when standardizing it.
- Keep changes limited to the relevant assertion-type folder and its environment-variable example entries.
- Preserve the existing Promptfoo schema declaration and conventions in neighboring configs.