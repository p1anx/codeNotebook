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
