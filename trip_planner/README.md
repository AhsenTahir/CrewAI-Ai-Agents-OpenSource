# AI Crew for Trip Planning
## Introduction
This project is a modified version of the CrewAI trip planner example, adapted to use Groq LLM for a more open-source approach. CrewAI orchestrates autonomous AI agents, enabling them to collaborate and execute complex tasks efficiently.

Original project by [@joaomdmoura](https://x.com/joaomdmoura)  
Modified to use Groq LLM

- [CrewAI Framework](#crewai-framework)
- [Running the script](#running-the-script)
- [Details & Explanation](#details--explanation)
- [Using Groq LLM](#using-groq-llm)
- [Contributing](#contributing)
- [Support and Contact](#support-and-contact)
- [License](#license)

## CrewAI Framework
CrewAI is designed to facilitate the collaboration of role-playing AI agents. In this example, these agents work together to choose between different cities and put together a full itinerary for the trip based on your preferences.

## Running the Script
This modified version uses Groq LLM for a more open and accessible approach.

### Prerequisites
1. Get your Groq API key from [Groq Cloud](https://console.groq.com/)
2. Set up accounts for additional services:
   - [Browseless](https://www.browserless.io/)
   - [Serper](https://serper.dev/)

### Setup Instructions
1. **Configure Environment**: 
   - Copy `.env.example` to `.env`
   - Set up the environment variables:
     ```
     GROQ_API_KEY=your_groq_api_key
     BROWSERLESS_API_KEY=your_browserless_key
     SERPER_API_KEY=your_serper_key
     ```
2. **Install Dependencies**: 
   ```bash
   poetry install --no-root
   ```
3. **Execute the Script**: 
   ```bash
   poetry run python main.py
   ```
   Follow the prompts to input your trip preferences.

## Details & Explanation
- **Key Components**:
  - `./main.py`: Main script file
  - `./trip_tasks.py`: Contains the tasks prompts
  - `./trip_agents.py`: Defines the agent creation and configuration
  - `./tools`: Contains tool classes used by the agents

## Using Groq LLM
This implementation uses Groq's LLM through the Langchain integration. The agents are configured to use Groq's models for enhanced performance and open-source compatibility.

Example configuration in the code:
```python
from langchain.chat_models import ChatGroq

llm = ChatGroq(
    api_key="your-groq-api-key",
    model_name="mixtral-8x7b-32768"
)

def local_expert(self):
    return Agent(
        role='Local Expert at this city',
        goal='Provide the BEST insights about the selected city',
        backstory="""A knowledgeable local guide with extensive information
        about the city, it's attractions and customs""",
        tools=[
            SearchTools.search_internet,
            BrowserTools.scrape_and_summarize_website,
        ],
        llm=llm,
        verbose=True
    )
```

## License
This project is released under the MIT License.
