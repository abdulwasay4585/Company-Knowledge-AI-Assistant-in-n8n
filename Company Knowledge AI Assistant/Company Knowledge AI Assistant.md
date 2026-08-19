# Company Knowledge AI Assistant

## Overview

Company Knowledge AI Assistant is a Retrieval Augmented Generation system built with n8n, Supabase and Google Gemini.

The system stores company knowledge in a vector database and uses semantic search to retrieve relevant information before generating an answer. This allows the AI assistant to answer questions using company specific knowledge instead of relying only on its general knowledge.

The project also includes a fallback response when the requested information cannot be found in the knowledge base.

## Architecture

```text
Company Knowledge
        ↓
Data Loader
        ↓
Text Splitter
        ↓
Gemini Embeddings
        ↓
Supabase Vector Database
        ↓
User Question
        ↓
AI Agent
        ↓
Supabase Vector Search
        ↓
Relevant Knowledge
        ↓
Gemini Chat Model
        ↓
Generated Answer
        ↓
Source / Fallback
```

## Technologies Used

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and AI orchestration |
| Supabase | Vector database and data storage |
| PostgreSQL | Database backend |
| pgvector | Vector storage and similarity search |
| Google Gemini | Embeddings and answer generation |
| AI Agent | Reasoning and tool selection |
| Recursive Character Text Splitter | Document chunking |

## Features

The system provides:

• Company knowledge ingestion

• Vector embeddings

• Semantic vector search

• Retrieval Augmented Generation

• AI generated answers

• Source information where available

• Fallback for unavailable information

• Conversation memory as an optional extension

• Human escalation as an optional extension

• Telegram or chat interface as an optional extension

## Knowledge Base

The project contains at least 20 company knowledge entries covering areas such as:

| Category | Example information |
|---|---|
| HR | Working hours |
| HR | Attendance |
| HR | Annual leave |
| HR | Sick leave |
| HR | Remote work |
| HR | Overtime |
| HR | Probation |
| HR | Promotions |
| IT | Password policy |
| IT | VPN access |
| IT | Laptop policy |
| IT | Software requests |
| IT | Security incidents |
| Finance | Salary payment |
| Finance | Expense reimbursement |
| Finance | Travel expenses |
| General | Office locations |
| General | Employee support |
| General | Company holidays |
| General | Office access |

## Vector Database

The company knowledge is stored in a Supabase table named:

```text
company_knowledge
```

The table contains:

```text
id
content
metadata
embedding
```

Metadata stores information such as:

```json
{
  "title": "Annual Leave",
  "category": "HR",
  "source": "Employee Handbook"
}
```

The embedding is generated from the knowledge content and stored in PostgreSQL using pgvector.

## RAG Process

The assistant follows this process:

```text
1. User asks a question
2. AI Agent receives the question
3. Vector Store Tool searches company knowledge
4. Relevant documents are retrieved
5. Retrieved information is provided to the AI model
6. Gemini generates the final answer
7. Source information is included when available
8. If sufficient information is not found, the fallback response is returned
```

## Fallback

The assistant must not invent company policies or information.

When the knowledge base does not contain enough information to answer a question, the assistant responds:

```text
Information not available in the company knowledge base.
```

Example:

```text
User:
Does the company provide free gym memberships?

Assistant:
Information not available in the company knowledge base.
```

## Example Queries

### Query 1

```text
How many days of annual leave do full time employees receive?
```

Expected result:

```text
Full time employees receive 20 days of annual paid leave per calendar year.

Source: Employee Handbook
```

### Query 2

```text
Can employees work from home?
```

Expected result:

```text
Eligible employees may work remotely up to two days per week with prior manager approval.

Source: Remote Work Policy
```

### Query 3

```text
What should I do if I receive a phishing email?
```

Expected result:

```text
Suspected security incidents such as phishing must be reported immediately to the IT security team.

Source: Information Security Policy
```

### Query 4

```text
How do I request new software?
```

Expected result:

```text
Employees should submit a software request through the IT service desk. IT reviews the request for licensing, security and compatibility requirements.

Source: IT Service Desk Guide
```

### Query 5

```text
How are business expenses reimbursed?
```

Expected result:

```text
Employees can request reimbursement for approved business expenses by submitting receipts and supporting documentation through the expense system.

Source: Expense Policy
```

### Query 6

```text
How long is the probation period?
```

Expected result:

```text
New employees normally complete a three month probation period.

Source: Employee Handbook
```

### Query 7

```text
Which cities have company offices?
```

Expected result:

```text
Northstar Technologies operates offices in Islamabad, Lahore and Karachi.

Source: Company Directory
```

### Query 8

```text
What are the normal working hours?
```

Expected result:

```text
Employees normally work from 9:00 AM to 5:00 PM, Monday through Friday.

Source: Employee Handbook
```

### Query 9

```text
What should I do if my company laptop is stolen?
```

Expected result:

```text
The assistant should retrieve the relevant company equipment and security information and provide only information supported by the knowledge base.
```

### Query 10

```text
Does the company provide free gym memberships?
```

Expected result:

```text
Information not available in the company knowledge base.
```

## AI Agent Rules

The AI Agent is instructed to:

```text
Use the company knowledge search tool for company related questions.

Do not invent company information.

Use retrieved information as the basis for answers.

Include the source when metadata is available.

Do not guess when information is missing.

Return "Information not available in the company knowledge base."
when the required information cannot be found.
```

## Optional Enhancements

The basic project can be extended with:

```text
Conversation Memory
        ↓
Remember previous questions and answers
```

```text
Human Escalation
        ↓
Send unresolved requests to HR or support
```

```text
Telegram Interface
        ↓
Ask questions through Telegram
```

These features are optional and are not required for the core RAG implementation.

## Project Result

The completed project demonstrates a complete company knowledge RAG pipeline:

```text
Knowledge Ingestion
        ↓
Embeddings
        ↓
Vector Database
        ↓
Semantic Retrieval
        ↓
AI Generation
        ↓
Source Attribution
        ↓
Fallback Handling
```

The result is a company specific AI assistant capable of answering questions from an internal knowledge base while reducing unsupported or hallucinated responses.

## Conclusion

The Company Knowledge AI Assistant demonstrates how n8n, Supabase, pgvector and Gemini can be combined to create a practical Retrieval Augmented Generation application.

The project satisfies the main requirements of the practical task by providing at least 20 knowledge entries, vector search, AI generated responses, source information and an explicit fallback when information is unavailable.