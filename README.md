# NPC Simulation Chatbot App

This project is a practice showcase project designed to build an interactive NPC (Non-Player Character) chatbot using ChatGPT, LangChain, and Streamlit. The primary goal is to create a dynamic chatbot that can simulate a character with varying moods and offer quests, all based on a user-uploaded character document.

## Project Overview

### Features
- **NPC Character Document Upload**: Option to upload a text document defining the NPC's character description, backstory, and available quests.
- **RAG-Based NPC Information Retrieval**: Utilizes Retrieval-Augmented Generation to answer user questions about the NPC and their world based on the character document.
- **Quest Offering System**: The NPC can offer quests defined in the uploaded document, managing quest availability and offering them contextually within conversations.
- **Mood-Based Conversational AI**: Implements a dynamic mood system (Happy, Neutral, Annoyed, Grumpy, Angry) influencing the NPC's responses.
- **Sentiment-Aware Interactions**: The chatbot analyzes user sentiment (rude, friendly, etc.) and adjusts the NPC's mood and responses accordingly.
- **Question Type Classification**: categorizes user questions to determine whether to provide general conversation, quest-related responses, or information retrieval.
- **Real-Time Conversational Interface**:  Built with Streamlit for a user-friendly, interactive chat experience.

## Why RAG and Streamlit?

This project leverages Retrieval-Augmented Generation (RAG) with LangChain and Streamlit for specific reasons that make them well-suited for creating interactive and informative NPC chatbots:

**Retrieval-Augmented Generation (RAG) with LangChain:**

- **Handling Extensive NPC Context:**  In game environments, NPCs often have a wealth of background information, including world lore, personal histories, knowledge of the player, and details about the game's progress.  RAG is ideal for managing this large volume of context. Instead of trying to cram all this information into the limited context window of a Large Language Model (LLM), RAG allows the chatbot to access and retrieve relevant pieces of information when answering user queries.
- **Improved Relevance and Reduced Hallucinations:** By grounding the NPC's responses in the provided character document and world information, RAG ensures that the chatbot's answers are more accurate, relevant, and consistent with the established lore. This significantly reduces the risk of the NPC "hallucinating" or inventing information that contradicts its defined persona or the game world.
- **Scalability for Rich Game Worlds:** RAG makes it feasible to build NPCs for complex and expansive game worlds. As the game world grows and NPC backstories become more detailed, the RAG system can be scaled to incorporate this increasing amount of information without hitting the limitations of LLM context windows. It allows for a continually expanding knowledge base for the NPC.
- **Dynamic Information Updates:** If the game world or NPC information changes (e.g., player progress unlocks new dialogue or world events alter NPC knowledge), the RAG system can be updated with new information, ensuring the NPC's knowledge remains current and reactive to the game state.

**Streamlit:**

- **Simple and Interactive UI:** Streamlit provides a straightforward way to create a user interface, making it perfect for showcasing the project and easily testing the NPC chatbot's functionality through a simple chat interface.


## **How It Works**

This application provides an interactive interface using **Streamlit** to engage in conversation with an NPC character defined by a document you upload. It allows you to experience dynamic interactions influenced by mood and quests, driven by AI. Here's how it functions:

1. **Upload Your NPC Character Document**
   - Upload a text file containing the NPC's character description, backstory/world information, and a list of quests.
   - The application parses this document to understand the NPC's persona and available quests.

2. **Character Setup and Knowledge Base**
   - The uploaded document is processed to extract key sections like "Character Description," "Backstory and World Info," and "Quests."
   - Backstory and world information are chunked and indexed into a **Vector database** using Chroma for efficient retrieval during information-seeking queries.

3. **Engage in Conversation**
   - Users can type questions or statements to interact with the NPC.
   - The system analyzes each user input to determine the question type and user sentiment.

4. **Question Classification and Sentiment Analysis**
   - The system categorizes the user's question into:
     - **Quest Request**: User is asking for a quest or offering help.
     - **Info Request**: User is asking about the NPC or their world.
     - **General Conversation**:  General greetings, small talk, or questions about the NPC's well-being.
   - Simultaneously, the user's message sentiment is classified as:
     - **Rude**: Disrespectful or insulting language.
     - **Neutral**:  Standard questions or statements.
     - **Friendly**: Polite and positive interactions.
     - **Apology**: User is apologizing.

5. **Processing the User Input**
   - Based on the question type and user sentiment, the system takes different actions:
     - **Quest Request**:
        - If the NPC is in a grumpy or angry mood, the quest request may be rudely refused.
        - If quests are available and the mood is acceptable, a quest is offered from the list in the document. Quests are offered only once per session.
        - If no quests are available, the NPC will indicate this, possibly with mood-appropriate dialogue.
     - **Info Request**: A RAG (Retrieval-Augmented Generation) chain is used to retrieve relevant information from the NPC's backstory and world information (vector database) to answer the user's question in character.
     - **General Conversation**: A general conversational chain is used to respond to the user in character, potentially weaving in subtle hints about available quests if contextually relevant and if the NPC is in a suitable mood.

6. **Mood Dynamics**
   - The NPC's mood (Happy, Neutral, Slightly Annoyed, Annoyed, Grumpy, Angry) is dynamically adjusted based on the user's sentiment.
   - Rude sentiment will worsen the mood, while friendly sentiment or apologies can improve it.
   - The current mood significantly impacts the NPC's responses, making interactions more engaging and varied.

7. **Display Results**
   - The chatbot's responses are displayed in real-time within the Streamlit app, creating an interactive and engaging conversation experience.


## Usage
- Run the [notebook ](https://github.com/SomersInias/NPC-RAG-Application/blob/main/notebooks/NPC_chatbot_app.ipynb) script in Google Colab.
- Provide your Open AI API key and ngrok API key.
- Run the Streamlit App: Run the full notebook
- Access via Public URL: URL provided by ngrok in your web browser
- Upload a text file defining your NPC character. Ensure the document follows the format the same the example npc [here](https://github.com/SomersInias/NPC-RAG-Application/blob/main/data/testnpc1.txt)
- Start chatting with your NPC by typing in the chat input box.

## Demo

