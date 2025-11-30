# **Project Title: Astro-Guard: Autonomous Multi-Agent Swarm for Aerospace Quality Control
Track: Enterprise Agents**

# **1. The Pitch**

## **Problem**
In high-stakes aerospace manufacturing, **quality assurance (QA) is the bottleneck. Human review of sensor telemetry is slow and prone to fatigue, while traditional automated thresholds miss complex, multi-variable failure modes** (e.g., a "thermal runaway" that is only dangerous when correlated with specific vibration harmonics). Missing these anomalies leads to catastrophic engine failure and millions in lost assets.

## **Solution**
Astro-Guard is an autonomous multi-agent system designed to act as an "always-on" reliability engineer. It ingests raw sensor data from rocket engine assembly lines (e.g., welding arms, thrust vector actuators) and processes it through a hierarchical agent swarm.

The system does not just flag errors; it reasons about them. It distinguishes between a harmless sensor glitch and a critical micro-fracture, searches for mitigation strategies using Google Search, and logs long-term predictive maintenance data.

## **Value**
Safety: Detects compound failure modes (Thermal + Vibration) that single-variable thresholds miss.

Efficiency: Uses a "Swarm" architecture to process data in parallel, reducing latency.

Cost Reduction: Implements custom token-optimization tools to minify JSON data before inference, significantly lowering API costs for high-throughput factories.

## **2. Technical Implementation & Architecture**
My submission demonstrates a sophisticated Hybrid Sequential-Parallel Architecture using the Google Gen AI SDK. I have implemented three (3) key concepts from the course:


### **Concept 1: Multi-Agent System (Parallel & Sequential Orchestration)**

I moved beyond a single-agent loop by implementing a hierarchical command structure:

The Parallel Sensing Swarm: I utilized the ParallelAgent class to deploy three highly specialized domain experts simultaneously:

Thermodynamic_Harmonic_Analyst: Monitors core temp and vibration for micro-fractures.

Hydro_Electric_Dynamics_Agent: Monitors power draw and hydraulic pressure for cavitation.

Metrology_Degradation_Forecaster: Tracks cycle counts to predict calibration drift.

Why this matters: By splitting these responsibilities, I can use smaller, faster models (gemini-2.5-flash-lite) for the sensors, reserving the reasoning power for the core analyzer.

The Sequential Reasoning Pipeline: The output of the swarm is fed into a SequentialAgent pipeline. The Meta_Analyzer_Core (powered by gemini-2.5-pro) synthesizes the three reports into a single actionable status (NOMINAL, WARNING, CRITICAL) before passing it to the Alert_Dispatch_Unit for formatting.


### **Concept 2: Tools (Built-in & Custom)**

I integrated tools to bridge the gap between static analysis and dynamic action:

Built-in Tool (Google Search): The Meta_Analyzer_Core is equipped with Google Search. If a failure mode is detected, the agent autonomously searches for known mitigation steps for that specific component failure, adding real-world context to the alert.

Custom Token-Optimization Tool (get_row_to_str): In manufacturing, data volume is high. I wrote a custom tool that serializes DataFrame rows into minified JSON strings to maximize token efficiency without losing data fidelity.

Custom Long-Term Memory Tool (log_critical_event): A custom Python function that appends critical failures to a persistent list (CRITICAL_FAILURE_LOGBOOK), allowing the system to maintain a record of severe incidents outside the ephemeral chat context.


### **Concept 3: Sessions & State Management**
The system is designed to be stateful, allowing operators to ask follow-up questions about specific alerts:

InMemorySessionService: I implemented the InMemorySessionService to manage conversation history. This allows the agent to "remember" the context of the previous analysis when the user asks follow-up questions (e.g., "Is there a failure in this row?" after a previous query).

Logbook Persistence: Beyond the session window, the Logbook_Integration_Agent acts as a bridge to long-term storage, ensuring that critical warnings are not lost when the session ends.


## **3. Deployment & Execution**
The agent is implemented as a Python notebook utilizing the Google Gen AI SDK.

Steps to Reproduce:

Environment: Requires Python 3.11+ and the google-genai and google-adk libraries.

Credentials: Set up a Kaggle Secret or Environment Variable for GOOGLE_API_KEY.

Data: The system expects a CSV file (rocket_engine_manufacturing.csv) containing telemetry (Timestamp, Core Temp, Vibration, etc.).

Execution:

Run the notebook cells to initialize the specialized agents.

The pipeline_agent will iterate through the DataFrame rows.

The system outputs structured logs and appends critical failures to CRITICAL_FAILURE_LOGBOOK.

Repository/Notebook Link: (Github)[https://github.com/AICoolK8e8vC83i/Astro-ManufacturiGuard-Autonomous-Multi-Agent-Swarm-for-Aerospace-Assistant]
