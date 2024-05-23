# Memories

Memories are pieces of text that are stored in a vector database (ChromaDB). Memories relevant to the current context
will be automatically injected into the prompt. Memories will also persist across restarts, unless manually deleted in
the frontend or the database is deleted.

The automatically generated memories are based off of 
[Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442). Essentially, 
every handful of messages, the LLM will be prompted to review the recent messages and come up with the 3 most high level
questions that encapsulate the conversation and also provide the answer. These question/answer pairs are then each
stored as a (short-term) memory. These short-term memories will persists across restarts unless deleted.

Memories are stored and loaded from the chroma.db file. However, if the database hasn't been created yet or is empty,
the program will load initial memories from the memoryinit.json file. This will NOT happen everytime the program starts, only
if the database is empty. You can also import/export memories to json.

The memories json file is in this format:

```json
{
  "memories": [
    {
      "id": "",
      "document": "",
      "metadata": {
        "type": "long-term"/"short-term"
      }
    },
    ...
  ]
}
```

The id can be any string but must be unique. The document is the text of the memory. The memories I manually add will
have human-friendly ids, but ids generated by the program are just UUIDs. The metadata indicates whether this memory is
long-term (manually added) or short-term (generated by the program). Long term and short term memories can be
controlled differently in the frontend.