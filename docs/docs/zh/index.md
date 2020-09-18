# 介绍

Poetry 是一个 Python 的依赖管理和打包工具。
它允许你为你的项目声明依赖库并对它们进行管理（安装/更新）。


## 系统要求

Poetry 需要 Python 2.7 或者 3.5+ 。它是多平台的，目标是在 Windows, Linux, OSX 工作得一样好。

!!! note
    
    Python 2.7 和 3.5 在下一个版本(1.2)将不会再被支持。
    你可以考虑更新 Python 版本至支持的版本。


## 安装


Poetry provides a custom installer that will install `poetry` isolated
from the rest of your system by vendorizing its dependencies. 这是推荐安装 `poetry` 的方法。

### osx / linux / bashonwindows 安装说明
```bash
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
```
### windows powershell 安装说明
```powershell
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python
```

!!! note
    
    你只需要安装一次 Poetry。它会自动选择当前版本的 Python ，并使用它[创建 virtualenvs](/docs/managing-environments)

安装程序会将 `poetry` 工具安装到 Poetry 的 `bin` 目录下。
在 Unix 下，它位于 `$HOME/.poetry/bin`，在 Windows 下 位于 `%USERPROFILE%\.poetry\bin`。

该目录将会在你的 `$PATH` 环境变量中。这意味你无需进一步的配置就能在 shell 中使用。
打开一个新的 shell 输入以下内容：

```bash
poetry --version
```

If you see something like `Poetry 0.12.0` then you are ready to use Poetry.
If you decide Poetry isn't your thing, you can completely remove it from your system
by running the installer again with the `--uninstall` option or by setting
the `POETRY_UNINSTALL` environment variable before executing the installer.

```bash
python get-poetry.py --uninstall
POETRY_UNINSTALL=1 python get-poetry.py
```

默认 Poetry 将会安装在平台特定(platform-specific)的 home 目录下。如果你想更改这个设定，你可以定义 `POETRY_HOME` 环境变量：

```bash
POETRY_HOME=/etc/poetry python get-poetry.py
```

如果你想安装预发行版本，你可以传递 `--preview` 参数给 `get-poetry.py` 或者使用 `POETRY_PREVIEW` 环境变量：

```bash
python get-poetry.py --preview
POETRY_PREVIEW=1 python get-poetry.py
```

同样，如果你想安装某个特定版本，你可以使用 `--version` 或者 `POETRY_VERSION` 环境变量：

```bash
python get-poetry.py --version 0.12.0
POETRY_VERSION=0.12.0 python get-poetry.py
```

!!!note

    注意这个安装程序不支持小于 0.12.0 版本的 Poetry

!!!note
    
    安装脚本必须能在你的 shell's path environment 下找到下列可执行文件之一：

    - `python` (which can be a py3 or py2 interpreter)
    - `python3`
    - `py.exe -3` (Windows)
    - `py.exe -2` (Windows)

### 替代安装方法（不推荐）

!!!note
    
    使用其他安装方法将使 Poetry 一直使用安装的 Python 版本创建虚拟环境。
    
    所以，如果你想要使用不同 Python 版本并进行切换。你需要为每个 Python 版本安装 Poetry。

#### 用 `pip` 进行安装

使用 `pip` 安装 Poetry 也是可行的。

```bash
pip install --user poetry
```

!!!warning
    
    注意这还会安装 Poetry 的依赖，可能会和其他包引发冲突。

#### 用 `pipx` 进行安装

使用 [`pipx`](https://github.com/cs01/pipx) 安装 Poetry 也是可行的。 
`pipx` 用于安装全局 Python CLI 程序但仍能将他们隔离在虚拟环境。这样可以进行干净地更新和卸载。
pipx 支持 Python 3.6 及更高版本。如果你使用更早期的 Python 版本，可以考虑使用 [pipsi](https://github.com/mitsuhiko/pipsi) 。

```bash
pipx install poetry
```

```bash
pipx upgrade poetry
```

```bash
pipx uninstall poetry
```

[Github repository](https://github.com/cs01/pipx).


## 更新 `poetry`

更新 Poetry 到最新版版就和调用 `self update` 命令一样简单。

```bash
poetry self update
```

如果你想安装预发行版本，你可以使用 `--preview` 选项。

```bash
poetry self update --preview
```

最后，如果你想安装特定版本，可以作为参数传递给 `self update`。

```bash
poetry self update 0.8.0
```

!!!note

    只有你使用推荐的安装方法安装 Poetry 时，`self update` 命令才会生效。

!!!note
    
    如果你的 poetry 版本还小于 1.0，你可以改用 `poetry self:update`。


## 为 Bash, Fish 或 Zsh 启用 tab 补全

`poetry` 支持为 Bash, Fish 和 Zsh generating completion scripts.
查询 `poetry help completions` 获取全部资料，但是要点很简单，如下所示：


```bash
# Bash
poetry completions bash > /etc/bash_completion.d/poetry.bash-completion

# Bash (Homebrew)
poetry completions bash > $(brew --prefix)/etc/bash_completion.d/poetry.bash-completion

# Fish
poetry completions fish > ~/.config/fish/completions/poetry.fish

# Fish (Homebrew)
poetry completions fish > (brew --prefix)/share/fish/vendor_completions.d/poetry.fish

# Zsh
poetry completions zsh > ~/.zfunc/_poetry

# Oh-My-Zsh
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry

# prezto
poetry completions zsh > ~/.zprezto/modules/completion/external/src/_poetry

```

!!! note
    
    为了使更改生效，你可能需要重启 shell。
    You may need to restart your shell in order for the changes to take effect.

对于 `zsh`， 你必须在 `~/.zshrc` 文件 `compinit` 前添加以下行： 

```bash
fpath+=~/.zfunc
```

对于 `oh-my-zsh`， 你必须在 `~/.zshrc` 插件中启用 `poetry`

```
plugins(
	poetry
	...
	)
```
