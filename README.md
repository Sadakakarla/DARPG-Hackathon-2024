# DARPG-Hackathon-2024

**PROBLEM STATEMENT:**
Develop an AI/ML-driven Chatbot that is ministry-specific to help the Citizens resolve their common queries related to filing a Grievance in the CPGRAMS portal (https://pgportal.gov.in) and expedite a smooth submission of grievances.

**Our Solution:**
This chatbot streamlines the grievance filing process for citizens on the CPGRAMS portal, providing detailed guidance and making the experience more user-friendly, even for those who prefer to converse in their native language.
This project implements an AI/ML-driven chatbot specifically designed to assist citizens with their common grievances related to the CPGRAMS portal (https://pgportal.gov.in). 

**Key features & techniques include:**

Mistral 7B LLM: Employs the powerful Mistral 7B HuggingFace Large Language Model for robust query understanding and response generation.
Contextual Learning: Parses CPGRAMS portal text and leverages a DARPG-provided Grievance Dataset to enhance the LLM's understanding of grievance filing procedures.

Retrieval Augmented Generation (RAG): Efficiently retrieves relevant information from an external database, ensuring accurate and informative responses to user queries.

**Specificity in Grievance Handling:** 

The chatbot is trained and equipped to address common grievance categories, including:
- Banking and financial transactions
- Passport issues
- Farmer/crop insurance concerns
- Railways and public transport issues
- Pension queries
- Internet and Broadband outages
- Many more types of grievances

**Multilingual Support:** To cater to a wider audience, the chatbot utilizes an Automatic Speech Recognition(ASR) pipeline. This pipeline detects the user's native language, enabling seamless interaction throughout the grievance filing process.

**Core Technique: Retrieval-Augmented Generation (RAG)**

At the heart of your solution lies the concept of RAG, a powerful technique for improving language model responses. 
It combines a prompt engineering approach with a custom dataset. In contrast to fine-tuning workflows, RAG workflows don’t require training of the model. Instead, the goal is to search for and merge relevant context from the dataset into the prompt fed to the model at generation time. 

RAGs extend prompt engineering by retrieving information relevant to a user’s prompt and augmenting the prompt that an LLM generates text to complete. The data being indexed, searched through, and retrieved as context is a collection of vectors, each representing a source object like a chunk of text, audio, or an image.

**Working of RAG:**

Retrieval ~ When a user asks a question, the system searches through a database of relevant information (CPGRAMS webpages, the preprocessed PDF of grievances data). This retrieval process is powered by tools like FAISS and the LangChain framework, using sentence-transformers to convert text into meaningful vector representations. The query is similarly turned into a vector and compared against the database for similarity, finding the most relevant sections of information.

Augmentation ~ The retrieved information isn't merely shown to the user. Instead, these relevant pieces of text are fed into a large language model (LLM), specifically the Mistral LLM in our case, along with the original user query as a prompt. The LLM uses this contextual information to generate a more accurate, informative, and tailored response than it could by relying on its general knowledge alone.

****Data Sources:****

A robust knowledge base incorporating different types of data:

**CPGRAMS Website:** https://pgportal.gov.in

Scraping webpages like the home page, FAQ, About Us, and Contact Us sections of the CPGRAMS portal provides foundational knowledge about the platform, its purpose, and its processes.

Here are the URLs that were passed to the LLM as its context base:

https://www.pgportal.gov.in/,
https://www.pgportal.gov.in/Home/Faq,
https://www.pgportal.gov.in/Home/AboutUs,
https://www.pgportal.gov.in/Home/ContactUs

**Preprocessed Grievances PDF:**
Analyzing past grievances data offers valuable insights into common issues, types of complaints, and the language citizens typically use to express their concerns.

**User Interface:**

We used Gradio for a Text-based Chat Interface:

Gradio's ChatInterface Component allows users to type in their queries as text or record their queries vocally, mimicking a natural dialogue experience.

**Functionality:**
Using the Gradio library, the interface is created which consists of two interactive tabs: Text and Audio.

**Text Tab:**
This tab utilizes a Chatbot component, allowing users to interact with a conversational AI system.
A Textbox component named "What is this document about?" is provided for users to input text.
When the user submits this text, a custom function (chat) is triggered, presumably responsible for processing the user input through the chatbot.

**Audio Tab:**
This tab provides an interface for audio transcription.
Users can upload audio files through an Audio component with the type set to "file path".
The code defines a function called 'transcribe' likely responsible for processing the uploaded audio and generating a text output.
This transcription functionality is enabled in "live" mode so that it can provide real-time results as the user speaks.
So any grievance query can be asked via a microphone or by uploading the audio file.

Steps involved:
- Capture audio input using the microphone.
- Convert the captured audio to text using the ASR pipeline.
- Pass the converted text to the LLM through the backend for processing and response generation.
- Display the LLM's response back to the user on the chat interface.


  


