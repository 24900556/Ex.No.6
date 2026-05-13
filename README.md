# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools


### Aim:
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

### AI Tools Required:

### Explanation:
Experiment the persona pattern as a programmer for any specific applications related with your interesting area. 
Generate the outoput using more than one AI tool and based on the code generation analyse and discussing that. 
### PROMPT:
Act as a Senior AI Software Architect, Python Developer, and Prompt Engineering Researcher. Design and develop a comprehensive Python-based multi-AI integration system capable of interacting with multiple AI tools and APIs to automate prompt execution, compare generated outputs, and generate analytical insights.

Create a Python application that connects with multiple AI tools/APIs, sends prompts automatically, collects generated responses, compares outputs, evaluates performance metrics, and generates actionable insights and analytical reports.

Integrate or simulate multiple AI tools including ChatGPT, Claude AI, Google Gemini, Perplexity AI, OpenAI API, and other relevant AI coding assistants.

Explain:

* Multi-AI integration systems
* API-based AI communication
* Importance of AI interoperability
* Role of Python in AI automation

Use the Persona Prompting Pattern by assigning the AI a specialized developer role such as:

* AI Research Engineer
* Cybersecurity Analyst
* Retail AI Developer
* Healthcare AI Assistant Developer
* Financial Data Analyst
* Robotics Software Engineer

Clearly explain:

* Why the selected persona was chosen
* How persona prompting affects code generation quality
* How different AI tools respond to the same persona prompt

Generate complete Python code for:

* API integration
* Sending prompts
* Receiving responses
* Error handling
* Logging outputs
* Comparing AI-generated results
* Exporting reports

The Python system must include:

* Modular architecture
* Reusable functions
* API request handling
* JSON processing
* Comparative evaluation engine
* Report generation module

Create multiple prompt experiments using:

* Broad prompts
* Refined prompts
* Role-based prompts
* Chain-of-thought prompts

For each AI tool:

* Send identical prompts
* Capture responses
* Compare:

  * Accuracy
  * Response speed
  * Depth
  * Logical reasoning
  * Code quality
  * Creativity
  * Error handling capability

Include the following experimental scenarios:

* AI Coding Assistant
* Healthcare AI
* Retail Automation
* Cybersecurity
* Data Analytics

Generate detailed comparison tables for:

* AI Tool Performance
* Code Accuracy
* Runtime Efficiency
* API Response Quality
* Context Understanding
* Error Management
* Scalability
* Security Considerations

Critically analyze:

* Differences in code generation styles
* Hallucination risks in generated code
* API reliability
* Token limitations
* Prompt sensitivity
* Multi-AI orchestration challenges
* Ethical considerations in AI-generated code

The generated Python implementation should include:

* requests library usage
* API authentication handling
* Environment variable management
* Exception handling
* CSV/JSON export
* Comparative scoring system
* Console-based dashboard or reporting interface

The final output must contain:

* Well-structured explanations
* Complete Python code
* Multiple AI-generated response simulations
* Comparative analytical tables
* Performance evaluation
* Findings and recommendations

Format the response as a professional technical report suitable for academic submission, AI research projects, software engineering demonstrations, and prompt engineering experiments. Ensure the output is highly detailed, technically advanced, logically structured, and implementation-oriented.
```
import asyncio
import time
import tkinter as tk
from tkinter import ttk, scrolledtext
from typing import List, Dict, Any
from abc import ABC, abstractmethod
import threading

# ==============================
# BASE AI ENGINE
# ==============================

class BaseAIEngine(ABC):
    """Abstract interface for all AI connectors."""

    def __init__(self, model_name: str):
        self.model_name = model_name

    @abstractmethod
    async def call_api(self, prompt: str) -> Dict[str, Any]:
        pass


# ==============================
# OPENAI CONNECTOR
# ==============================

class OpenAIConnector(BaseAIEngine):

    async def call_api(self, prompt: str) -> Dict[str, Any]:

        start = time.perf_counter()

        await asyncio.sleep(0.5)

        return {
            "model": self.model_name,
            "latency": round(time.perf_counter() - start, 3),
            "logic_score": 0.95,
            "response": f"GPT-4o analyzed prompt:\n'{prompt}'\nOptimized solution generated."
        }


# ==============================
# CLAUDE CONNECTOR
# ==============================

class ClaudeConnector(BaseAIEngine):

    async def call_api(self, prompt: str) -> Dict[str, Any]:

        start = time.perf_counter()

        await asyncio.sleep(0.7)

        return {
            "model": self.model_name,
            "latency": round(time.perf_counter() - start, 3),
            "logic_score": 0.98,
            "response": f"Claude 3.5 analyzed prompt:\n'{prompt}'\nNuanced reasoning provided."
        }


# ==============================
# GEMINI CONNECTOR
# ==============================

class GeminiConnector(BaseAIEngine):

    async def call_api(self, prompt: str) -> Dict[str, Any]:

        start = time.perf_counter()

        await asyncio.sleep(0.6)

        return {
            "model": self.model_name,
            "latency": round(time.perf_counter() - start, 3),
            "logic_score": 0.93,
            "response": f"Gemini Pro analyzed prompt:\n'{prompt}'\nEfficient modular approach suggested."
        }


# ==============================
# MULTI AI ORCHESTRATOR
# ==============================

class MultiAIOrchestrator:

    def __init__(self, engines: List[BaseAIEngine]):
        self.engines = engines

    async def benchmark(self, prompt: str):

        tasks = [engine.call_api(prompt) for engine in self.engines]

        results = await asyncio.gather(*tasks)

        return self.generate_insights(results)

    def generate_insights(self, results: List[Dict]):

        best_logic = max(results, key=lambda x: x['logic_score'])

        fastest = min(results, key=lambda x: x['latency'])

        insights = {
            "logic_leader": best_logic,
            "speed_leader": fastest,
            "results": results
        }

        return insights


# ==============================
# GUI APPLICATION
# ==============================

class MultiAIGUI:

    def __init__(self, root):

        self.root = root
        self.root.title("🚀 Multi-AI Benchmark Dashboard")
        self.root.geometry("950x700")
        self.root.configure(bg="#0f172a")

        title = tk.Label(
            root,
            text="🚀 Multi-AI Benchmark Dashboard",
            font=("Arial", 22, "bold"),
            bg="#0f172a",
            fg="#38bdf8"
        )

        title.pack(pady=15)

        # Prompt Label
        prompt_label = tk.Label(
            root,
            text="Enter Prompt:",
            font=("Arial", 12),
            bg="#0f172a",
            fg="white"
        )

        prompt_label.pack()

        # Prompt Input
        self.prompt_entry = scrolledtext.ScrolledText(
            root,
            width=100,
            height=5,
            font=("Arial", 11)
        )

        self.prompt_entry.pack(pady=10)

        # Analyze Button
        analyze_btn = tk.Button(
            root,
            text="Analyze with AI Models",
            font=("Arial", 12, "bold"),
            bg="#38bdf8",
            fg="white",
            padx=15,
            pady=8,
            command=self.run_analysis_thread
        )

        analyze_btn.pack(pady=10)

        # Results Area
        self.results_box = scrolledtext.ScrolledText(
            root,
            width=110,
            height=25,
            font=("Consolas", 10),
            bg="#1e293b",
            fg="white"
        )

        self.results_box.pack(pady=15)

    # ==========================
    # THREAD HANDLER
    # ==========================

    def run_analysis_thread(self):

        thread = threading.Thread(target=self.run_analysis)

        thread.start()

    # ==========================
    # RUN ANALYSIS
    # ==========================

    def run_analysis(self):

        prompt = self.prompt_entry.get("1.0", tk.END).strip()

        if not prompt:
            return

        self.results_box.delete("1.0", tk.END)

        self.results_box.insert(tk.END, "⏳ Running Multi-AI Benchmark...\n\n")

        asyncio.run(self.process_prompt(prompt))

    # ==========================
    # PROCESS PROMPT
    # ==========================

    async def process_prompt(self, prompt):

        orchestrator = MultiAIOrchestrator([

            OpenAIConnector("GPT-4o"),

            ClaudeConnector("Claude 3.5 Sonnet"),

            GeminiConnector("Gemini Pro")

        ])

        analysis = await orchestrator.benchmark(prompt)

        self.display_results(analysis)

    # ==========================
    # DISPLAY RESULTS
    # ==========================

    def display_results(self, analysis):

        self.results_box.insert(tk.END, "\n=============================\n")
        self.results_box.insert(tk.END, "📊 AI MODEL COMPARISON RESULTS\n")
        self.results_box.insert(tk.END, "=============================\n\n")

        for result in analysis["results"]:

            self.results_box.insert(tk.END, f"🤖 Model: {result['model']}\n")

            self.results_box.insert(
                tk.END,
                f"⚡ Latency: {result['latency']} sec\n"
            )

            self.results_box.insert(
                tk.END,
                f"🧠 Logic Score: {result['logic_score']}\n"
            )

            self.results_box.insert(
                tk.END,
                f"💬 Response:\n{result['response']}\n"
            )

            self.results_box.insert(
                tk.END,
                "\n--------------------------------------\n\n"
            )

        # Comparative Insights
        self.results_box.insert(
            tk.END,
            "\n🏆 COMPARATIVE INSIGHTS\n"
        )

        self.results_box.insert(
            tk.END,
            "=============================\n"
        )

        logic = analysis["logic_leader"]

        speed = analysis["speed_leader"]

        self.results_box.insert(
            tk.END,
            f"🧠 Logic Leader: {logic['model']} "
            f"(Score: {logic['logic_score']})\n"
        )

        self.results_box.insert(
            tk.END,
            f"⚡ Speed Leader: {speed['model']} "
            f"(Latency: {speed['latency']} sec)\n"
        )


# ==============================
# MAIN APPLICATION
# ==============================

if __name__ == "__main__":

    root = tk.Tk()

    app = MultiAIGUI(root)

    root.mainloop()
```
### OUTPUT:

<img width="1920" height="1140" alt="image" src="https://github.com/user-attachments/assets/cbc34b53-3ceb-46d7-b5f9-d363dc689501" />


### Result:
The corresponding Prompt is executed successfully.
