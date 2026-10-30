---
name: cognee-recall-google
description: "Retrieve information from Cognee datasets, permanent memory, and session history using the recall tool. Trigger when the user asks to search Cognee, recall memory, or query datasets."
---
# Cognee Recall Skill

Use `recall()` as the primary tool to retrieve information from Cognee datasets, searching both permanent memory and session history.

## When to Use

- The user asks to search Cognee datasets or retrieve memory.
- You need to recall past context, conversation history, or specific dataset information.

## Core Workflow

1. **Formulate:** Create a clear, targeted `query_text` based on the user's prompt.
2. **Retrieve:** Call `recall()` with the appropriate parameters, actively scoping the search to reduce noise.
3. **Synthesize:** Use the retrieved context to answer the user, citing the specific sources.

## Key Parameters

- `query_text` (str): The main question or search phrase.
- `datasets` (list): Restrict retrieval to specific datasets (e.g., `datasets=["Semester_1_Computer"]`). If omitted, it searches across all datasets the user can read.
- `session_id` (str): Include to search session cache and conversation history. Session results are tagged with `source="session"`, and graph results with `source="graph"`.
- `query_type` (enum): Optional. Forces a specific retrieval mode (e.g., `SearchType.GRAPH_COMPLETION`).
- `top_k` (int): Control the number of results returned.
- `only_context` (bool): Set to `True` when you want the raw retrieved context instead of an auto-generated answer.

## Best Practices & Gotchas

- **Scope aggressively:** Always scope queries to a specific dataset (`datasets`) or `session_id` when possible to improve relevance and reduce noise.
- **Handle empty results:** If the initial search yields empty results, retry using broader search terms or a different `query_type`.
- **Cite your sources:** Include the `source` field in your final answer citations to clearly indicate where the information originated.
