# Encurtador de Links

Este é um aplicativo de desktop em Python que permite encurtar URLs e copiar o link encurtado para a área de transferência. Utiliza a biblioteca `pyshorteners` para encurtar URLs e `pyperclip` para copiar para a área de transferência. A interface gráfica foi criada com `tkinter`.

## Funcionalidades

- **Encurtar Links:** Insira uma URL e obtenha um link encurtado.
- **Copiar Links:** Copie o link encurtado para a área de transferência com um clique.

## Tecnologias Utilizadas

- Python
- Tkinter (para interface gráfica)
- Pyshorteners (para encurtar URLs)
- Pyperclip (para copiar para a área de transferência)

## Pré-requisitos

- Python 3.x
- Bibliotecas Python:
  - `pyshorteners`
  - `pyperclip`
  - `tkinter` (inclusa por padrão em Python)

## Instalação

1. Clone o repositório:
    ```bash
    git clone https://github.com/seu-usuario/encurtador-de-links.git
    cd encurtador-de-links
    ```

2. Instale as dependências:
    ```bash
    pip install pyshorteners pyperclip
    ```

## Uso

1. Execute o script:
    ```bash
    python encurtador_de_links.py
    ```

2. Insira a URL que você deseja encurtar e clique no botão "Encurtar".
3. O link encurtado será exibido e você poderá copiá-lo para a área de transferência clicando no botão "Copiar".

## Código Exemplo

```python
import tkinter as tk
from tkinter import messagebox
import pyshorteners
import pyperclip  # Biblioteca para copiar para a área de transferência

# Função para encurtar o link
def encurtar_link():
    url = entrada_link.get()
    if url:
        try:
            s = pyshorteners.Shortener()
            link_encurtado = s.tinyurl.short(url)
            resultado.config(text=f"Link Encurtado: {link_encurtado}")
            entrada_link_encurtado.delete(0, tk.END)  # Limpar a caixa de texto
            entrada_link_encurtado.insert(0, link_encurtado)  # Exibir o link encurtado na caixa de texto
        except Exception as e:
            messagebox.showerror("Erro", f"Ocorreu um erro: {str(e)}")
    else:
        messagebox.showerror("Erro", "Por favor, insira um link.")

# Função para copiar o link encurtado para a área de transferência
def copiar_link():
    link_encurtado = entrada_link_encurtado.get()
    if link_encurtado:
        pyperclip.copy(link_encurtado)
        messagebox.showinfo("Copiado", "Link encurtado copiado para a área de transferência.")

# Configuração da janela
janela = tk.Tk()
janela.title("Encurtador de Links")

# Rótulo e entrada para o link original
rotulo_link = tk.Label(janela, text="Insira o link:")
rotulo_link.pack(pady=10)
entrada_link = tk.Entry(janela, width=40)
entrada_link.pack()

# Botão para encurtar o link
botao_encurtar = tk.Button(janela, text="Encurtar", command=encurtar_link)
botao_encurtar.pack(pady=10)

# Rótulo para exibir o link encurtado
resultado = tk.Label(janela, text="")
resultado.pack()

# Caixa de texto para o link encurtado
entrada_link_encurtado = tk.Entry(janela, width=40)
entrada_link_encurtado.pack()

# Botão para copiar o link encurtado
botao_copiar = tk.Button(janela, text="Copiar", command=copiar_link)
botao_copiar.pack(pady=10)

# Iniciar a interface gráfica
janela.mainloop()
