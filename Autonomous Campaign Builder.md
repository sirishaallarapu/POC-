# 🚀 Autonomous Campaign Builder
This project is an AI-powered system that transforms a marketing goal into a complete, ready-to-launch campaign plan using a series of intelligent LangGraph agents. Each agent specializes in a specific marketing function—from market research to content creation, audience segmentation, simulation, and email outreach.

Powered by LangChain, LangGraph, ChromaDB, and Gemini Pro, the system ensures every decision is grounded in data and optimized for performance.

---

## 📌 Objective

To build an intelligent, end-to-end system that:

- Understands high-level business goals (e.g., “Increase SUV sales in South-West”).
- Analyzes past sales, customer, and campaign data using semantic search.
- Segments target audiences automatically.
- Suggests marketing strategies and generates content.
- Simulates campaign performance and exports a structured plan.

---

## ⚙️ Technologies and Packages Used

| Purpose                | Tool / Package                  |
|------------------------|---------------------------------|
| Language               | Python                          |
| LLM                    | Gemini-Pro (via LangChain)      |
| Embeddings             | textembedding-gecko-004 (Google)|
| Vector Database        | ChromaDB                        |
| Workflow Framework     | LangChain + LangGraph           |
| Data Handling          | Pandas                          |
| Environment Variables  | python-dotenv                   |
| File Handling          | os, json                        |

> ✅ [Install Python](https://www.python.org/downloads/)

---

## 📥 Environment Setup

Install required packages via pip:

pip install numpy>=1.24.0
pip install pandas>=2.0.0
pip install langchain>=0.1.0
pip install langchain-community>=0.0.10
pip install langchain-core>=0.1.0
pip install langchain-google-genai>=0.0.5
pip install langgraph>=0.0.15
pip install chromadb>=0.4.22
pip install python-dotenv>=1.0.0
pip install pydantic>=2.0.0
pip install tenacity>=8.0.0
pip install streamlit>=1.22.0

## Datasets Used:
customer.csv → Contains details like customer ID, region, gender, preferences, etc.

sales.csv → Information on products sold, purchase dates, and regions.

marketing_campaign.csv → Past campaign types, communication channels, and outcomes.

## Data Chunking & Embedding Strategy
Each row from the dataset is transformed into a sentence using Python string formatting. These chunks make it easier for the model to semantically understand and embed the information.
 Example:
Original Row:
customer_id,region,gender,car_preference
C101,North,Female,SUV
Chunked Sentence:
"Customer C101 from North region is a Female who prefers SUV."

Embedding and Vector Storage:
These generated sentences are embedded using Google’s textembedding-gecko-004 model, which converts them into high-dimensional vectors. This allows similarity search and reasoning across related pieces of information.

These text chunks are embedded using Google’s textembedding-gecko-004 model and stored in ChromaDB collections:
customer_data
sales_data
campaign_data

## Project Workflow Overview
🔄 Goal-to-Campaign Flow
1.	Input: A business goal (e.g., "Boost SUV sales in South-West")
2.	Agent Workflow: Managed by LangGraph to process the goal through these stages:

	Agent name                           Responsibility

create_campaign_strategy	         Creates campaign structure: name, timeline, channels, KPIs, messaging
generate_content	                 Crafts content for email, social, and landing pages
generate_final_report	             Compiles all generated assets into a detailed campaign report
research_market_trends	             Uses Tavily + internal data to generate market and trend analysis
segment_audience	                 Selects ideal primary and secondary audience segments based on goal and market insights
send_emails                        	 Sends personalized marketing emails to target customers using campaign content
simulate_campaign	                 Predicts campaign performance by estimating reach, engagement, conversions, ROI, risks,         
                                     and improvements.

3.	Context: Each agent uses relevant data from ChromaDB, powered by semantic search.


## Agent Workflow & Architecture
The project follows a Goal-to-Campaign Flow powered by LangChain and LangGraph. Each goal is processed through a sequence of intelligent agents, with decisions enhanced by semantic search using ChromaDB and Google embeddings.

   +-------------------------+
   |  User Campaign Goal     |
   +-----------+-------------+
               |
        [LangGraph Orchestration]
               |
+--------------v--------------+
|       create_strategy Agent |
+--------------+--------------+
               |
+--------------v--------------+
|     generate_content Agent  | ← Pulls from ChromaDB
+--------------+--------------+
               |
+--------------v--------------+
|    generate_report Agent    |
+--------------+--------------+
               |
+--------------v--------------+
|     research_market Agent   |
+--------------+--------------+
               |
+--------------v--------------+
|    segment_audience Agent   |
+--------------+--------------+
               |
+--------------v--------------+
|      send_emails Agent      |
+--------------+--------------+
               |
+--------------v--------------+
|    simulate_campaign Agent  |
+-----------------------------+


## Example Use Case
**Goal:** "Promote Electric SUVs to eco-conscious buyers in South India."

| Agent Name               | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| research_market_trends   | Finds EV adoption trends, top cities, and seasonal interest spikes         |
| segment_audience         | Identifies ideal customer segments (e.g., urban eco-conscious men 30–45)  |
| create_campaign_strategy | Builds the campaign: name, timeline, channels (email/social), KPIs        |
| generate_content         | Writes emails, social posts, and landing pages tailored to segments        |
| simulate_campaign        | Predicts reach, clicks, conversions, ROI, and campaign risks               |
| send_emails              | Sends personalized emails using generated content to matched customers      |
| generate_final_report    | Compiles strategy, content, and performance into a final campaign report   |

## ## ✅ Conclusion

This project automates end-to-end campaign creation using AI agents and LangGraph. From goal parsing to strategy, content, simulation, and personalized outreach — every step is intelligently handled. It's modular, scalable, and designed for rapid, data-driven marketing execution.
