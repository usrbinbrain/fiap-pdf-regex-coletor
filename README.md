# fiap-pdf-regex-coletor

## Descrição

Este script Python, chamado `regex_coletor.py`, foi criado para extrair informações específicas de um arquivo PDF, mais especificamente números de telefone e endereços de e-mail contidos em qualquer página do arquivo. Isso é feito usando expressões regulares, ou 'regex', que são sequências de caracteres que formam um padrão de pesquisa.

## Dependências

Este script depende das seguintes bibliotecas Python:

- `re`: Esta é uma biblioteca integrada do Python, portanto, você não precisa instalá-la. Ela é usada para trabalhar com expressões regulares (regex) no Python.
- `sys`: Assim como a `re`, essa também é uma biblioteca padrão do Python, usada para interagir com o sistema operacional.
- `PyPDF2`: Essa biblioteca externa é usada para ler arquivos PDF no Python.

### Como instalar as dependências

Como as bibliotecas `re` e `sys` já estão integradas no Python, você só precisa instalar a `PyPDF2`. Para fazer isso, abra seu terminal e digite o seguinte comando:

```bash
pip install PyPDF2
```

Se você estiver usando um sistema operacional baseado em Unix (como o Linux ou MacOS), você pode precisar usar `pip3` no lugar de `pip`.

## Uso

Para usar este script, você precisa passar o nome do arquivo PDF como um argumento de linha de comando. Por exemplo, se você tem um arquivo chamado `documento.pdf` na mesma pasta do script, você pode rodar o script assim:

```bash
python3 regex_coletor.py documento.pdf
```

O script irá imprimir os números de telefone e os endereços de e-mail que encontrou no arquivo PDF.

## Como o script funciona

1. Primeiro, o script define um conjunto de expressões regulares para reconhecer números de telefone e endereços de e-mail.

2. Em seguida, o script abre o arquivo PDF fornecido e lê o conteúdo de cada página.

3. Ele procura por números de telefone e endereços de e-mail em cada página, usando as expressões regulares definidas anteriormente.

4. Por fim, ele imprime todas as correspondências encontradas.



## O script

```bash
#!/usr/bin/env python3

# Importando as bibliotecas necessárias
import re
import sys
from PyPDF2 import PdfReader

# Definindo a função que irá extrair as informações
def extract_info_from_pdf(pdf_filename):
    # Abrindo o arquivo PDF
    pdf_file = open(pdf_filename, 'rb')
    # Criando um objeto PdfReader, que permite ler o conteúdo do arquivo PDF
    pdf_reader = PdfReader(pdf_file)

    # Listas para armazenar os telefones e e-mails encontrados
    phones = []
    emails = []

    # Definindo as expressões regulares para números de telefone e e-mails
    phone_regex = r'[+]?[(][0-9]{1,4}[)]?[-\s./0-9]*'
    email_regex = r'[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]*'

    # Iterando sobre cada página do PDF
    for page in pdf_reader.pages:
        # Extraindo o texto da página
        text = page.extract_text()

        # Procurando por telefones e e-mails na página e adicionando-os às listas
        phones.extend(re.findall(phone_regex, text))
        emails.extend(re.findall(email_regex, text))

    # Fechando o arquivo PDF
    pdf_file.close()

    # Retornando as listas de telefones e e-mails
    return phones, emails

# Usando a função para extrair as informações do PDF cujo nome foi passado como argumento de linha de comando
phones, emails = extract_info_from_pdf(sys.argv[1])

# Imprimindo os telefones e e-mails encontrados
print(f"\nTelefones encontrados: {phones}")
print(f"\nEmails encontrados: {emails}")
```
