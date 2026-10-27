<p align="center">
    <img src="https://raw.githubusercontent.com/EduPekUfpr/PythonProject/refs/heads/main/Images/BannerUFPR.png" width="700" alt="PPGOLD/PPGMNE Python:INTRO"  />
</p>

## Prof. Eduardo Pécora, Ph.D.

# **Instalando Python e Jupyter no seu computador**

**Disciplina:** Python e Pandas para Análise de Dados  
**Material de apoio (opcional):** as aulas usam o Google Colab, que não exige instalação. Este guia é para quem quiser trabalhar também no próprio computador.

### Objetivos
Ao final deste guia você terá:

1. Python instalado no **Windows**, **macOS** ou **Linux**;
2. Um **ambiente** exclusivo para a disciplina, com NumPy, Pandas, Matplotlib, Seaborn e Jupyter;
3. O **JupyterLab** abrindo os notebooks do curso localmente;
4. Uma checagem final confirmando que tudo funciona.

### Neste guia
| Passo | Tema | Tempo estimado |
|:---:|---|:---:|
| 1 | [Antes de começar: o que vamos instalar](#antes) | 3 min |
| 2 | Instalar o Miniforge: [Windows](#windows), [macOS](#macos) ou [Linux](#linux) | 10 min |
| 3 | [Criar o ambiente da disciplina](#ambiente) | 5 min |
| 4 | [Abrir o JupyterLab](#jupyter) | 2 min |
| 5 | [Verificar a instalação](#verificar) | 2 min |
| — | [Alternativa: python.org + pip](#alternativa) · [VS Code](#vscode) · [Problemas comuns](#problemas) | — |

Ao final estão as [referências](#referencias).

<a id="antes"></a>

---
## 1. Antes de começar: o que vamos instalar

Vamos usar o **Miniforge**, uma distribuição leve e gratuita do Python que traz o gerenciador de pacotes **conda**. Escolhemos o Miniforge porque:

- o procedimento é **praticamente igual** nos três sistemas;
- **não exige permissão de administrador**;
- instala pacotes do repositório comunitário **conda-forge**, sem as restrições de licença do Anaconda.

Depois criaremos um **ambiente** só para a disciplina. Um ambiente é uma instalação isolada do Python com seus próprios pacotes, parecida com o `renv` do R: o que você instalar nele não interfere em outros projetos.

| Componente | Para que serve |
|---|---|
| Python | a linguagem |
| conda (via Miniforge) | instala pacotes e cria ambientes |
| NumPy, Pandas | cálculo vetorizado e manipulação de dados |
| Matplotlib, Seaborn | gráficos |
| JupyterLab | interface de notebooks no navegador, como o Colab |

> **Versão do Python:** usaremos o **Python 3.13**. Versões recém-lançadas podem ainda não ter todos os pacotes disponíveis, por isso não use necessariamente a mais nova do site.

Escolha o seu sistema e siga **apenas** a seção correspondente: [Windows](#windows) · [macOS](#macos) · [Linux](#linux).

<a id="windows"></a>

---
## 2a. Windows

1. Acesse [conda-forge.org/download](https://conda-forge.org/download/) e baixe o instalador **`Miniforge3-Windows-x86_64.exe`**.
2. Execute o arquivo baixado. Se o Windows exibir o aviso "O Windows protegeu o computador", clique em **Mais informações → Executar assim mesmo**.
3. Aceite a licença (**I Agree**).
4. Selecione **Just Me (recommended)**.
5. Mantenha a pasta sugerida, por exemplo `C:\Users\seu_nome\miniforge3`.
   > ⚠️ Se o seu nome de usuário tiver **espaços ou acentos** (ex.: `C:\Users\João Silva`), troque a pasta para **`C:\miniforge3`**. Caminhos com esses caracteres causam erros no conda.
6. Na tela de opções avançadas, **mantenha os padrões** (não é preciso marcar "Add Miniforge3 to my PATH").
7. Clique em **Install** e, ao final, em **Finish**.
8. No menu Iniciar, procure e abra o **Miniforge Prompt**. É nele que você digitará os comandos deste guia.
9. Confirme a instalação digitando:
   ```
   conda --version
   ```
   Deve aparecer algo como `conda 25.x.x`.

Agora siga para o [passo 3: criar o ambiente](#ambiente).

<a id="macos"></a>

---
## 2b. macOS

1. Descubra o processador do seu Mac: menu **Apple () → Sobre este Mac**.
   - **Chip Apple M1, M2, M3, M4…** → Apple Silicon (`arm64`)
   - **Processador Intel** → `x86_64`
2. Abra o **Terminal** (`Cmd + Espaço`, digite "Terminal" e tecle Enter).
3. Baixe e execute o instalador com os comandos abaixo, que detectam o processador automaticamente:
   ```bash
   cd ~/Downloads
   curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
   bash Miniforge3-$(uname)-$(uname -m).sh
   ```
   > Se preferir baixar pelo navegador: em [conda-forge.org/download](https://conda-forge.org/download/), escolha `Miniforge3-Darwin-arm64.sh` (Apple Silicon) ou `Miniforge3-Darwin-x86_64.sh` (Intel) e rode o terceiro comando com o nome do arquivo baixado.
4. Durante a instalação:
   - pressione **Enter** para ler a licença (barra de espaço avança, `q` sai) e digite **`yes`** para aceitar;
   - pressione **Enter** para aceitar a pasta padrão (`~/miniforge3`);
   - quando perguntar se deve inicializar o conda (*initialize*), digite **`yes`**.
5. **Feche e abra o Terminal de novo.** O início da linha deve mostrar `(base)`.
6. Confirme a instalação:
   ```bash
   conda --version
   ```

> **Alternativa com Homebrew:** se você já usa o [Homebrew](https://brew.sh), basta `brew install --cask miniforge` seguido de `conda init zsh`, e depois reabrir o Terminal.

Agora siga para o [passo 3: criar o ambiente](#ambiente).

<a id="linux"></a>

---
## 2c. Linux

Os comandos abaixo funcionam em Ubuntu, Debian, Fedora, Mint e na maioria das distribuições.

1. Abra um terminal (no Ubuntu: `Ctrl + Alt + T`).
2. Baixe e execute o instalador:
   ```bash
   cd ~/Downloads
   curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
   bash Miniforge3-$(uname)-$(uname -m).sh
   ```
   > Se não tiver o `curl`, use `wget` no lugar de `curl -L -O`, ou instale-o com `sudo apt install curl` (Ubuntu/Debian).
3. Durante a instalação:
   - pressione **Enter**, leia a licença e digite **`yes`**;
   - pressione **Enter** para aceitar a pasta padrão (`~/miniforge3`);
   - quando perguntar se deve inicializar o conda, digite **`yes`**.
4. **Feche e abra o terminal de novo.** O início da linha deve mostrar `(base)`.
5. Confirme a instalação:
   ```bash
   conda --version
   ```

> Não use `sudo` para instalar o Miniforge: ele foi feito para ficar na sua pasta de usuário.

<a id="ambiente"></a>

---
## 3. Criar o ambiente da disciplina (todos os sistemas)

A partir daqui os comandos são **iguais** nos três sistemas. No Windows use o **Miniforge Prompt**; no macOS e no Linux, o **Terminal**.

**3.1 Crie o ambiente** `curso-python` com o Python 3.13 e os pacotes da disciplina (leva alguns minutos):
```bash
conda create -n curso-python python=3.13 numpy pandas matplotlib seaborn jupyterlab notebook ipykernel -y
```

**3.2 Ative o ambiente:**
```bash
conda activate curso-python
```
O início da linha muda de `(base)` para `(curso-python)`. **Você precisa ativar o ambiente toda vez que abrir um novo terminal.**

**3.3 Precisa de outro pacote depois?** Com o ambiente ativo:
```bash
conda install nome-do-pacote
```
Se o pacote não existir no conda-forge, use `pip install nome-do-pacote` (sempre com o ambiente ativo).

| Comando útil | O que faz |
|---|---|
| `conda env list` | lista os ambientes |
| `conda list` | lista os pacotes do ambiente ativo |
| `conda deactivate` | sai do ambiente |
| `conda env remove -n curso-python` | apaga o ambiente (para recomeçar do zero) |

<a id="jupyter"></a>

---
## 4. Abrir o JupyterLab

1. No terminal, **ative o ambiente** e vá até a pasta onde estão (ou ficarão) os notebooks do curso. Exemplo:
   ```bash
   conda activate curso-python
   cd Documentos/curso-python
   ```
   > Dica: crie antes uma pasta só para a disciplina e salve nela os `.ipynb` baixados do Colab (*Arquivo → Fazer download → Fazer o download do .ipynb*).
2. Inicie o JupyterLab:
   ```bash
   jupyter lab
   ```
3. O navegador abre sozinho em `http://localhost:8888`. Se não abrir, copie o endereço com `token=` que aparece no terminal e cole no navegador.
4. Para criar um notebook: **File → New → Notebook** e escolha o kernel **Python 3**.
5. **Não feche o terminal** enquanto estiver usando o Jupyter. Para encerrar, salve os notebooks e, no terminal, pressione `Ctrl + C` (confirme com `y` se pedir).

> Prefere a interface clássica, parecida com a do Colab? Use `jupyter notebook` em vez de `jupyter lab`.

Os atalhos de teclado que você aprendeu no Colab são quase os mesmos no Jupyter (`Shift + Enter` executa; no modo de comando, `A`/`B` criam células acima/abaixo e `M`/`Y` alternam entre markdown e código).

<a id="verificar"></a>

---
## 5. Verificar a instalação

1. Baixe o notebook [`verificar_instalacao.ipynb`](verificar_instalacao.ipynb) desta pasta e salve-o na pasta da disciplina.
2. Com o ambiente ativo, abra o JupyterLab nessa pasta (`jupyter lab`) e abra o notebook.
3. Execute a célula (`Shift + Enter`). Todos os pacotes devem aparecer com versão, e um gráfico deve ser exibido.

O código executado é este:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt
import seaborn as sns

print(f"Python     {sys.version.split()[0]}")
print(f"NumPy      {np.__version__}")
print(f"Pandas     {pd.__version__}")
print(f"Matplotlib {matplotlib.__version__}")
print(f"Seaborn    {sns.__version__}")
print("Ambiente:", sys.prefix)

x = np.linspace(0, 2 * np.pi, 100)
fig, ax = plt.subplots(figsize=(6, 3))
ax.plot(x, np.sin(x))
ax.set_title("Instalação OK!")
plt.show()
```

> Se aparecer `ModuleNotFoundError`, o notebook provavelmente está usando o Python errado. Veja [Problemas comuns](#problemas).

<a id="alternativa"></a>

---
## Alternativa: Python oficial (python.org) + pip

Para quem prefere não usar o conda. Funciona bem, mas os passos variam mais entre sistemas.

**Windows**
1. Baixe o instalador do **Python 3.13** em [python.org/downloads](https://www.python.org/downloads/).
2. Na primeira tela, **marque "Add python.exe to PATH"** e clique em *Install Now*.
3. Abra o **Prompt de Comando** ou o **PowerShell** e rode:
   ```
   py -3.13 -m venv curso-python
   curso-python\Scripts\activate
   pip install numpy pandas matplotlib seaborn jupyterlab
   jupyter lab
   ```
   > No PowerShell, se aparecer erro de "execução de scripts desabilitada", rode uma vez `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`.

**macOS**
1. Baixe o instalador do **Python 3.13** (*macOS 64-bit universal2 installer*) em [python.org/downloads](https://www.python.org/downloads/) e instale.
2. No Terminal:
   ```bash
   python3.13 -m venv curso-python
   source curso-python/bin/activate
   pip install numpy pandas matplotlib seaborn jupyterlab
   jupyter lab
   ```

**Linux (Ubuntu/Debian)**
```bash
sudo apt update
sudo apt install python3 python3-venv python3-pip
python3 -m venv curso-python
source curso-python/bin/activate
pip install numpy pandas matplotlib seaborn jupyterlab
jupyter lab
```
> Nesse caso a versão do Python é a da sua distribuição. Qualquer versão a partir da 3.11 atende à disciplina.

Nas três opções, o comando `activate` precisa ser repetido a cada novo terminal, como no conda.

<a id="vscode"></a>

---
## Opcional: usar o VS Code em vez do navegador

O [Visual Studio Code](https://code.visualstudio.com/) abre arquivos `.ipynb` diretamente e é uma boa opção para quem também vai escrever scripts.

1. Instale o VS Code.
2. Na aba **Extensions** (`Ctrl + Shift + X`; no Mac, `Cmd + Shift + X`), instale as extensões **Python** e **Jupyter**, ambas da Microsoft.
3. Abra um `.ipynb` e clique em **Select Kernel** (canto superior direito) → **Python Environments** → escolha **curso-python**.

<a id="problemas"></a>

---
## Problemas comuns

| Sintoma | Causa provável | Solução |
|---|---|---|
| `conda` não é reconhecido como comando (Windows) | Comando digitado no Prompt de Comando comum | Use o **Miniforge Prompt** do menu Iniciar |
| `zsh: command not found: conda` / `bash: conda: command not found` | O terminal não foi reaberto, ou o conda não foi inicializado | Feche e abra o terminal. Se persistir: `~/miniforge3/bin/conda init zsh` (macOS) ou `~/miniforge3/bin/conda init bash` (Linux) |
| `ModuleNotFoundError: No module named 'pandas'` | Ambiente não ativado antes de abrir o Jupyter, ou kernel errado | Feche o Jupyter, rode `conda activate curso-python` e depois `jupyter lab`. No VS Code, troque o kernel para **curso-python** |
| Erros estranhos na instalação no Windows | Pasta com espaços ou acentos | Reinstale o Miniforge em `C:\miniforge3` |
| `jupyter lab` abre na porta 8889 em vez de 8888 | Já há outro Jupyter aberto | Não é erro. Use o endereço indicado no terminal ou feche o outro Jupyter |
| O navegador não abre | Configuração do sistema | Copie o endereço `http://localhost:8888/lab?token=...` do terminal |
| Não encontro meus arquivos no Jupyter | O Jupyter mostra só a pasta onde foi iniciado | Encerre (`Ctrl + C`), use `cd` até a pasta certa e rode `jupyter lab` de novo |

Se nada resolver, recomece o ambiente: `conda env remove -n curso-python` e repita o [passo 3](#ambiente). Enquanto isso, o Colab continua disponível para acompanhar as aulas.

<a id="referencias"></a>

---
## Referências

**Miniforge e conda**
- [conda-forge: download do Miniforge](https://conda-forge.org/download/)
- [Repositório oficial do Miniforge (instruções detalhadas)](https://github.com/conda-forge/miniforge)
- [Documentação do conda: gerenciando ambientes](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

**Python — documentação oficial**
- [Downloads do Python](https://www.python.org/downloads/)
- [Usando o Python no Windows](https://docs.python.org/pt-br/3/using/windows.html)
- [Usando o Python em um Mac](https://docs.python.org/pt-br/3/using/mac.html)
- [Usando o Python em plataformas Unix](https://docs.python.org/pt-br/3/using/unix.html)
- [Ambientes virtuais e pacotes (`venv` e `pip`)](https://docs.python.org/pt-br/3/tutorial/venv.html)

**Jupyter e editores**
- [Documentação do JupyterLab](https://jupyterlab.readthedocs.io/en/stable/)
- [Jupyter Notebooks no VS Code](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)

## Fique Conectado

- [![YouTube](https://img.icons8.com/?size=40&id=19318&format=png&color=000000)](https://www.youtube.com/@LigaDataScience/videos)  
  Explore nossos vídeos educacionais e webinars sobre ciência de dados, machine learning e inteligência artificial. Inscreva-se para não perder nenhuma atualização!

- [![LinkedIn](https://img.icons8.com/?size=40&id=13930&format=png&color=000000)](https://www.linkedin.com/company/liga-data-science-ufpr/)  
  Siga-nos no LinkedIn para as últimas novidades, oportunidades de carreira e networking profissional no campo da ciência de dados.

- [![Instagram](https://img.icons8.com/?size=40&id=32323&format=png&color=000000)](https://www.instagram.com/ligadatascience/)  
  Confira nosso Instagram para conteúdos dos bastidores, destaques de eventos e o dia a dia da Liga Data Science. Faça parte da nossa jornada!

## Autores

<a href="https://www.linkedin.com/in/eduardopecora/" target="_blank">Eduardo Pecora</a>

## Log de modificações

| Data | Versão | Modificado por | Descrição |
| ----------------- | ------- | ---------- | ---------------------------------- |
| 27-10-2026 | 1.0 | Claude (a pedido de Eduardo Pécora) | Guia inicial de instalação do Python e Jupyter (Windows, macOS e Linux), em notebook |
| 27-10-2026 | 1.1 | Claude (a pedido de Eduardo Pécora) | Convertido para Markdown (`INSTALACAO.md`); checagem separada em `verificar_instalacao.ipynb` |

<hr>

## <h3 align="center"> (c) Liga Data Science/ UFPR 2026. All rights reserved. <h3/>
