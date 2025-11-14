# 🎬 The Film Director Agent

A powerful, multi-step AI orchestration agent designed to generate detailed, cinematic short stories and film treatments from a single theme. This agent uses a structured workflow to ensure narrative coherence, deep character development, and high-quality final output.

## ✨ Features

* **🎬 Structured Workflow:** Utilizes a pipeline of specialized sub-agents for plot generation, character creation, and final story assembly.
* **✍️ Detailed Narrative:** Produces a complete cinematic story (approx. 1000–2000 words) with vivid world-building and dramatic progression.
* **👤 Deep Characterization:** Generates compelling characters tailored specifically to the initial plot idea.
* **⚡️ Optimized for Speed:** Built upon efficient models (`gemini-2.5-flash` and `gemini-2.0-flash-lite`) for rapid prototyping.

## ⚙️ How It Works (The Agent Pipeline)

The `Film_writer` acts as the orchestrator, guiding the execution through three distinct phases:

| Phase | Agent | Model | Task | Output Key |
| :--- | :--- | :--- | :--- | :--- |
| **1. Plot Generation** | `ContentWriter` | `gemini-2.5-flash-lite` | Generates a concise (100-150 word) base plot from the user's theme. | `basic_content` |
| **2. Character Development**| `Character_Developer` | `gemini-2.5-flash-lite` | Creates 3-5 detailed characters based on the base plot (`basic_content`). | `Characters` |
| **3. Final Assembly** | `Film_writer` | `gemini-2.5-flash` | Integrates `basic_content` and `Characters` into the final, complete cinematic story. | `Full_film_story` |

## 🚀 Getting Started

### Prerequisites

1.  **Python:** Ensure you have Python 3.9+ installed.
2.  **Agent Development Kit (ADK):** This project requires the Google Agent Development Kit for execution.
    ```bash
    pip install google-adk
    ```
3.  **API Key:** Set your Gemini API key as an environment variable.
    ```bash
    export GEMINI_API_KEY="YOUR_API_KEY"
    ```

### Running the Agent

Assuming your agent definitions are in a file named `film_agent.py`:

1.  **Import and Initialize:**
    ```python
    from film_agent import Film_writer
    from google.adk.runners import InMemoryRunner

    # 1. Initialize the Runner
    runner = InMemoryRunner(agent=Film_writer) 
    
    # 2. Define the Theme
    theme = "A lone explorer discovers a forgotten city beneath the Antarctic ice, guarded by an ancient AI."
    
    # 3. Run the Agent (using async/await if in an async environment)
    import asyncio
    
    async def main():
        print(f"Running agent for theme: {theme}")
        response = await runner.run_debug(theme)
        print("\n--- FINAL FILM SCRIPT SUMMARY ---\n")
        print(response.text)

    # Execute the main function
    if __name__ == "__main__":
        asyncio.run(main())
    ```

## 📂 Code Structure

The project relies on the following key components defined in your code:

* `basic_content_writer`: Agent for initial plot.
* `Character_Developer`: Agent for character creation.
* `Film_writer`: The master orchestrator agent (using the `gemini-2.5-flash` model).

## 🤝 Contributing

We welcome contributions! If you have suggestions for new sub-agents (e.g., a "Dialogue Polisher" or "Setting Designer"), please open an issue or submit a pull request.

---

*Built with the Gemini API and Google ADK.*
