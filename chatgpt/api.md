# Get started
```python
import openai
# add 'export OPENAI_API_KEY="your_api_key"' in .bashrc or .zshrc
client = openai.OpenAI()
# 使用指定模型创建聊天完成任务
stream = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[{"role": "user", "content": "Say this is a test"}],
    stream=True,
)
for chunk in stream:
    if chunk.choices[0].delta.content is not None:
        print(chunk.choices[0].delta.content, end="")
```
# litellm
## example 1
usage with streaming
```python
from litellm import completion
import os

## set ENV variables
# os.environ["OPENAI_API_KEY"] = "your-openai-key"
# os.environ["ANTHROPIC_API_KEY"] = "your-cohere-key"

messages = [
    { "content": "you are a translate assistant","role": "system"},
    { "content": "翻译为中文： how are you?","role": "user"},
    { "content": "再翻译为韩语","role": "user"},
]
response = completion(model="openai/gpt-4o-mini", messages=messages, stream=True)
# print(response.choices[0].message.content, end = '\n')
for part in response:
    print(part.choices[0].delta.content, end = "")

# # openai call
# response = completion(model="openai/gpt-4o-mini", messages=messages)
#
# # anthropic call
# # response = completion(model="anthropic/claude-3-sonnet-20240229", messages=messages)
# print(response)

```
usage without streaming
```python
from litellm import completion
import os

## set ENV variables
# os.environ["OPENAI_API_KEY"] = "your-openai-key"
# os.environ["ANTHROPIC_API_KEY"] = "your-cohere-key"

messages = [
    { "content": "you are a translate assistant","role": "system"},
    { "content": "翻译为中文： how are you?","role": "user"},
    { "content": "再翻译为韩语","role": "user"},
]
response = completion(model="openai/gpt-4o-mini", messages=messages)
print(response.choices[0].message.content, end = '\n')# this part is different

#
# # anthropic call
# # response = completion(model="anthropic/claude-3-sonnet-20240229", messages=messages)
# print(response)

```

