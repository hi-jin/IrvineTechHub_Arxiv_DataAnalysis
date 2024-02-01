# Introduction

## [purpose] The reason for analyzing `arxiv` webpage

If you're a researcher, you've used the arxiv website.  
I always follow the trend topic, but I couldn't confirm it as true even if I felt that the topic was a trend.  
I wanted to check the thesis trend through a survey on the number of papers by keyword.

## [structure]
```python
class ArxivResult:
    id: int
    title: str
    authors: T.List[str]
    link: str
    tags: T.List[str]
    originally_announced_at: str

class ConcatedArxivResult:
    id_for_search_keyword: int
    title: str
    authors: T.List[str]
    link: str
    tags: T.List[str]
    search_keyword: str
    submitted: str
    originally_announced: str
```
ArxivResult is the result format for one search keyword.  
ConcatedArxivResult is the concated format. (arxiv_papers.csv)

## Analysis

![](./analysis.png)
Methodologies that appeared before transformers, such as rnn, lstm, gru, and so on, appear to have fewer and fewer keywords.  

On the other hand, LLM and reinforcement learning, which are hot keywords in recent years, are showing a very high rise.

## Key Features (Scraping Method)
### Fast Scraps with *Multi-Threading*
```python
...

queues = [queue.Queue() for _ in range(N_THREADS)]
threads = []

for i in range(N_THREADS):
    thread = th.Thread(target=get_arxiv_results, args=(YEAR, search_idx, item_idx, TERMS, queues[i]))
    thread.start()
    threads.append(thread)

    ...

...
```

### Stable development through type hints
- classes, `import typing`, ...
