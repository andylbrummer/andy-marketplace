---
name: tokenize
description: Tokenize text with various tokenizers
---

# Text Tokenization

Tokenize text using GPT, SentencePiece, or custom tokenizers.

## Usage

Provide text and tokenizer to get token IDs and statistics.

## Examples

**GPT-2 tokenizer:**
```
/llm-mcp:tokenize "Hello, world!" with gpt2
```

**Custom BPE:**
```
/llm-mcp:tokenize corpus.txt with bpe vocab_size=8000
```

**Analyze tokens:**
```
/llm-mcp:tokenize document.txt and show token distribution
```

## MCP Tools

**Tokenize text:**
```
Call: mcp__llm-mcp__tokenize_text
Parameters: {
  "text": "<text to tokenize>",
  "tokenizer": "<gpt2|tiktoken|sentencepiece|custom>"
}
```

**Train tokenizer:**
```
Call: mcp__llm-mcp__train_tokenizer
Parameters: {
  "corpus_path": "<path to training corpus>",
  "vocab_size": <target vocabulary size>,
  "tokenizer_type": "<bpe|unigram|wordpiece>"
}
```

## Tokenizers

| Type | Description |
|------|-------------|
| `gpt2` | GPT-2 BPE tokenizer |
| `tiktoken` | OpenAI tiktoken (cl100k_base, etc.) |
| `sentencepiece` | Google SentencePiece |
| `custom` | User-trained tokenizer |
