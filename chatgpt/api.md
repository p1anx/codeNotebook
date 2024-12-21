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
# read from PDF
```python
import PyPDF2
class ToMarkdown:
    def __init__(self, md_file_path):
        self.md_file = md_file_path
    def saveas_markdown(self, text):
        with open(self.md_file, 'w', encoding = 'utf-8') as file:
            file.write('# tile1\n')
            file.write(text)
            file.write('\n\n')
        print('write over!!!')
        


# 打开 PDF 文件
file = 'demo.pdf'
# 创建 PDF 阅读器对象
pdf_reader = PyPDF2.PdfReader(file)

# 获取 PDF 页数
num_pages = len(pdf_reader.pages)

# 读取每一页的内容
text = ""
print("pages =", num_pages)
for page_num in range(num_pages):
    page = pdf_reader.pages[page_num]
    text += page.extract_text()  # 提取文本
```
