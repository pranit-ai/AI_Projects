# SQL AI Agent

## Overview

This project showcases an **AI-powered workflow** that utilizes natural language processing to generate and run SQL queries on an SQLite database. The workflow is designed using **n8n**, an open-source automation tool, and integrates OpenAI for query formulation and execution. The result is presented in a structured table format, and the data is saved as a **CSV** for easy access.

## Files Included

1. **SQL_AI_Agent.png**  
   - This file contains a screenshot of the **n8n workflow** demonstrating how natural language inquiries are processed and converted into SQL queries using OpenAI.

2. **northwind.db**  
   - This is the **SQLite database** file that is queried by the AI agent. It contains sample data on which SQL queries are executed.

3. **query_result_northwind.csv**  
   - This file contains the **output results** from running SQL queries. It is generated in a structured table format, saved for easy reference, and accessible for download.

## Features

- **Natural Language Query Input:**  
  The workflow allows users to input natural language queries through a **Chat UI** (e.g., "Show me customers from the UK"). The system then translates these into SQL queries.

- **OpenAI Integration for Prompt Engineering:**  
  Using **prompt engineering**, OpenAI is utilized to generate precise SQL queries based on user requests, ensuring accurate and reliable results.

- **SQLite Database Querying:**  
  The system connects to an **SQLite database** (northwind.db) to run the queries formulated by OpenAI, ensuring the data is pulled from a real-world, structured data source.

- **CSV Export:**  
  The results are displayed in a **structured markdown table** format in the Chat UI and saved as a **CSV file** for easy sharing, analysis, and storage.

## Skills Highlighted

- **Prompt Engineering:**  
  Leveraged OpenAI's capabilities to craft tailored prompts for generating accurate and context-aware SQL queries based on natural language input.

- **AI Agent Development:**  
  Developed a seamless workflow that integrates **AI-driven query formulation** and **automated data retrieval** using n8n and OpenAI's models.

- **Database Querying:**  
  Worked with **SQLite** for database querying and handling structured data in real-time.

- **Automation Tools:**  
  Utilized **n8n** for automation of the workflow, ensuring seamless interaction between the Chat UI, OpenAI, and the SQLite database.

# Conclusion

This project demonstrates the power of AI-driven automation in making database querying accessible and efficient for non-technical users. By combining natural language processing with SQL querying and database management, users can easily retrieve and analyze data without needing advanced technical knowledge.
