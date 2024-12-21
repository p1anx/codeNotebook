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
# simple usage of langchain
```python
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage
%%time 
chat = ChatOpenAI(model="gpt-4o-mini", temperature=0.2)
response = chat.invoke(
    [
        HumanMessage(
            content="Translate this sentence from English to Chinese: I love programming."
        )
    ]
)
print(response.content)
response = chat.invoke([HumanMessage(content="What did you just say?")])
print(response.content)

response = chat.invoke(
    [
        HumanMessage(
            content="Translate this sentence from English to French: I love programming."
        ),
        # AIMessage(content="J'adore la programmation."),
        HumanMessage(content="What did you just say?"),
    ]
)
print(response.content)
```
#  chatgpt template for research pdf 
```python
from langchain.chains import ConversationChain
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage
from langchain.memory import ConversationBufferMemory

from langchain_openai import ChatOpenAI
from PyPDF2 import PdfReader
class pdf:
    def __init__(self,file_path):
        self.file = file_path
    def read(self, fileName):
        pdf_file = PdfReader(fileName)
        num_pages = len(pdf_file.pages)
        text = ""
        for page_n in range(1):
            page = pdf_file.pages[page_n]
            text += page.extract_text()
        # print(text)
        return text
class chat:

    def output():
        pdf_file = 'demo.pdf'
        output_md_name = 'demo.md'
        pdf_content = pdf(pdf_file).read(pdf_file)
        message0 = "您是一名经验丰富的研究学者，我将会发送一些学术文献给您，请您仔细阅读文献内容，并为我详细讲解文献的各个部分，解答我的疑问。这对我非常重要，因此我希望您能够认真对待，确保每个问题都能得到准确和深入的回答。完成任务后，我将给予丰厚的报酬。注意！请您详细阅读文章内容，不要偷懒！并用中文回答我的问题。"
        message1 = f"请您概述一下这篇文章的主要内容。要求总结准确全面，涵盖文章的核心观点和结论，并用简洁明了的语言进行描述。文章内容：{pdf_content}"
        message2 = "请您说明该篇文章主要研究的核心问题是什么，并简要概述作者为何选择研究这个问题，以及该问题在该领域的重要性"
        message3 = ""


        message = [message0, message1, message2]
        llm = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)
        conversation = ConversationChain(
            llm=llm,
            verbose=False,
            memory=ConversationBufferMemory()
        )
        response_text = ""
        for message_n in message:
            response = conversation.invoke(input = message_n)
            response_text +=response['response']
            print(response['response'], end = '\n')

        ToMarkdown(output_md_name).saveas_markdown(response_text)
# conversation.predict(input="Tell me about yourself.")
# print(response)
class ToMarkdown:
    def __init__(self, md_file_path):
        self.md_file = md_file_path
    def saveas_markdown(self, text):
        with open(self.md_file, 'w', encoding = 'utf-8') as file:
            file.write('# tile1\n')
            file.write(text)
            file.write('\n\n')
        print('write over!!!')
if __name__ == "__main__":
    chat.output()

```
