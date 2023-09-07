<h1 align="center">● Open Interpreter</h1>

<p align="center">
    <a href="https://discord.gg/YG7APUyJ5"><img alt="Discord" src="https://img.shields.io/discord/1146610656779440188?logo=discord&style=flat&logoColor=white"></a> <img src="https://img.shields.io/static/v1?label=license&message=MIT&color=white&style=flat" alt="License">
<br>
    <b>Let language models run code on your computer.</b><br>
    An open-source, locally running implementation of OpenAI's Code Interpreter.<br>
    <br><a href="https://openinterpreter.com">Get early access to the desktop application.</a><br>
</p>

## windows虚拟环境安装记录

- windows下使用conda虚拟环境安装open-interpreter，并本地部署Code-Llama的注意事项
- 具体创建虚拟环境请搜索相关教程
- 创建虚拟环境后需要提前使用pip安装 `pip install llama-cpp-python`，本地编译时可能报错，原因是未安装C++环境，需要安装微软的Visual Studio C++工具：https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/
- 上述完成后安装open-interpreter，`pip install open-interpreter`
- 安装完毕之后执行 `interpreter -l` 运行本地模型，根据提示选择模型版本和是否使用GPU等。首次运行指定模型需要下载，请确保网络环境配置正确。
  - 模型选择后会将模型下载到 `C:\Users\{用户名}\AppData\Local\Open Interpreter\Open Interpreter\models`
  - 因为是C盘路径，一般总容量比较吃紧，如果需要修改模型地址，应该是需要手动修改源代码了，源代码文件 `interpreter/llama_2.py`。或者修改APPDATA环境变量(不过尝试了一下无效)
    ```python
    # Get user data directory
    user_data_dir = appdirs.user_data_dir("Open Interpreter")
    default_path = os.path.join(user_data_dir, "models")
    ```
  - 一旦中途失败，将会重新下载模型而不是断点续传，如果选择较大模型，请确保网络通畅，或者直接使用别的下载器下载相应的模型，放到上述文件夹中，避免浪费时间。各个版本模型下载地址如下：
    ```python
    models = {
        '7B': {
            'Low': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-7B-Instruct-GGUF/resolve/main/codellama-7b-instruct.Q3_K_S.gguf', 'Size': '3.01 GB', 'RAM': '5.51 GB'},
            'Medium': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-7B-Instruct-GGUF/resolve/main/codellama-7b-instruct.Q4_K_M.gguf', 'Size': '4.24 GB', 'RAM': '6.74 GB'},
            'High': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-Instruct-7B-GGUF/resolve/main/codellama-7b-instruct.Q8_0.gguf', 'Size': '7.16 GB', 'RAM': '9.66 GB'}
        },
        '13B': {
            'Low': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/resolve/main/codellama-13b-instruct.Q3_K_S.gguf', 'Size': '5.66 GB', 'RAM': '8.16 GB'},
            'Medium': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/resolve/main/codellama-13b-instruct.Q4_K_M.gguf', 'Size': '8.06 GB', 'RAM': '10.56 GB'},
            'High': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-13B-Instruct-GGUF/resolve/main/codellama-13b-instruct.Q8_0.gguf', 'Size': '13.83 GB', 'RAM': '16.33 GB'}
        },
        '34B': {
            'Low': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-34B-Instruct-GGUF/resolve/main/codellama-34b-instruct.Q3_K_S.gguf', 'Size': '14.21 GB', 'RAM': '16.71 GB'},
            'Medium': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-34B-Instruct-GGUF/resolve/main/codellama-34b-instruct.Q4_K_M.gguf', 'Size': '20.22 GB', 'RAM': '22.72 GB'},
            'High': {'URL': 'https://huggingface.co/TheBloke/CodeLlama-34B-Instruct-GGUF/resolve/main/codellama-34b-instruct.Q8_0.gguf', 'Size': '35.79 GB', 'RAM': '38.29 GB'}
        }
    }
    ```
- 模型下载完毕后就可以愉快的使用了，更多使用说明见原始仓库：[open-interpreter](https://github.com/KillianLucas/open-interpreter)
- 如果不需要使用本地模型，请忽略上述说明，按原仓库说明使用，需要申请OpenAi的API KEY

<br>

![poster](https://github.com/KillianLucas/open-interpreter/assets/63927363/08f0d493-956b-4d49-982e-67d4b20c4b56)

<br>

```shell
pip install open-interpreter
```

```shell
interpreter
```

<br>

**Open Interpreter** lets LLMs run code (Python, Javascript, Shell, and more) locally. You can chat with Open Interpreter through a ChatGPT-like interface in your terminal by running `$ interpreter` after installing.

This provides a natural-language interface to your computer's general-purpose capabilities:

- Create and edit photos, videos, PDFs, etc.
- Control a Chrome browser to perform research
- Plot, clean, and analyze large datasets
- ...etc.

**⚠️ Note: You'll be asked to approve code before it's run.**

<br>

## Demo

https://github.com/KillianLucas/open-interpreter/assets/63927363/37152071-680d-4423-9af3-64836a6f7b60

#### An interactive demo is also available on Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1WKmRXZgsErej2xUriKzxrEAXdxMSgWbb?usp=sharing)

## Quick Start

```shell
pip install open-interpreter
```

### Terminal

After installation, simply run `interpreter`:

```shell
interpreter
```

### Python

```python
import interpreter

interpreter.chat("Plot APPL and META's normalized stock prices") # Executes a single command
interpreter.chat() # Starts an interactive chat
```

## Comparison to ChatGPT's Code Interpreter

OpenAI's release of [Code Interpreter](https://openai.com/blog/chatgpt-plugins#code-interpreter) with GPT-4 presents a fantastic opportunity to accomplish real-world tasks with ChatGPT.

However, OpenAI's service is hosted, closed-source, and heavily restricted:
- No internet access.
- [Limited set  of pre-installed packages](https://wfhbrian.com/mastering-chatgpts-code-interpreter-list-of-python-packages/).
- 100 MB maximum upload, 120.0 second runtime limit.
- State is cleared (along with any generated files or links) when the environment dies.

---

Open Interpreter overcomes these limitations by running on your local environment. It has full access to the internet, isn't restricted by time or file size, and can utilize any package or library.

This combines the power of GPT-4's Code Interpreter with the flexibility of your local development environment.

## Commands

#### Interactive Chat

To start an interactive chat in your terminal, either run `interpreter` from the command line:

```shell
interpreter
```

Or `interpreter.chat()` from a .py file:

```python
interpreter.chat()
```

#### Programmatic Chat

For more precise control, you can pass messages directly to `.chat(message)`:

```python
interpreter.chat("Add subtitles to all videos in /videos.")

# ... Streams output to your terminal, completes task ...

interpreter.chat("These look great but can you make the subtitles bigger?")

# ...
```

#### Start a New Chat

In Python, Open Interpreter remembers conversation history. If you want to start fresh, you can reset it:

```python
interpreter.reset()
```

#### Save and Restore Chats

`interpreter.chat()` returns a List of messages when return_messages=True, which can be used to resume a conversation with `interpreter.load(messages)`:

```python
messages = interpreter.chat("My name is Killian.", return_messages=True) # Save messages to 'messages'
interpreter.reset() # Reset interpreter ("Killian" will be forgotten)

interpreter.load(messages) # Resume chat from 'messages' ("Killian" will be remembered)
```

#### Customize System Message

You can inspect and configure Open Interpreter's system message to extend its functionality, modify permissions, or give it more context.

```python
interpreter.system_message += """
Run shell commands with -y so the user doesn't have to confirm them.
"""
print(interpreter.system_message)
```

#### Change the Model

> Note: We're working on consolidating these into a unified command.

You can run `interpreter` in local mode from the command line to use `Code Llama`:

```shell
interpreter --local
```

For `gpt-3.5-turbo`, use fast mode:

```shell
interpreter --fast
```

In Python, you will need to set the model manually:

```python
interpreter.model = "gpt-3.5-turbo"
```

#### Azure Support

To connect to an Azure deployment, the `--use-azure` flag will walk you through setting this up:

```
interpreter --use-azure
```

In Python, set the following variables:

```
interpreter.use_azure = True
interpreter.api_key = "your_openai_api_key"
interpreter.azure_api_base = "your_azure_api_base"
interpreter.azure_api_version = "your_azure_api_version"
interpreter.azure_deployment_name = "your_azure_deployment_name"
```

#### Debug mode

To help contributors inspect Open Interpreter, `--debug` mode is highly verbose. 

You can activate debug mode by using it's flag (`interpreter --debug`), or mid-chat:

```
$ interpreter
...
> %debug # <- Turns on debug mode
```

## Safety Notice

Since generated code is executed in your local environment, it can interact with your files and system settings, potentially leading to unexpected outcomes like data loss or security risks.

**⚠️ Open Interpreter will ask for user confirmation before executing code.**

You can run `interpreter -y` or set `interpreter.auto_run = True` to bypass this confirmation, in which case:

- Be cautious when requesting commands that modify files or system settings.
- Watch Open Interpreter like a self-driving car, and be prepared to end the process by closing your terminal.
- Consider running Open Interpreter in a restricted environment like Google Colab or Replit. These environments are more isolated, reducing the risks associated with executing arbitrary code.

## How Does it Work?

Open Interpreter equips a [function-calling language model](https://platform.openai.com/docs/guides/gpt/function-calling) with an `exec()` function, which accepts a `language` (like "python" or "javascript") and `code` to run.

We then stream the model's messages, code, and your system's outputs to the terminal as Markdown.

## Contributing

This is a community-made project. If it looks exciting to you, please don't hesitate to contribute!

## License

Open Interpreter is licensed under the MIT License. You are permitted to use, copy, modify, distribute, sublicense and sell copies of the software.

**Note**: This software is not affiliated with OpenAI.
> Having access to a junior programmer working at the speed of your fingertips ... can make new workflows effortless and efficient, as well as open the benefits of programming to new audiences.
>
> — _OpenAI's Code Interpreter Release_

<br>
