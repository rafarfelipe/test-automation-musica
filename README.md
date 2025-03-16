# Parodify Robot

Este projeto utiliza o Robot Framework para automatizar testes no site Parodify.

## Estrutura do Projeto

```
player.robot
logs/
    log.html
    output.xml
    playwright-log.txt
    report.html
    browser/
        screenshot/
            robotframework-browser-screenshot-1.png
        traces/
            temp/
                86088b51-0809-4a1f-bd90-15d080561b02/
resources/
    module.js
```

## Requisitos

- Python 3.13.2
- Robot Framework 7.2.2
- Biblioteca Browser para Robot Framework

## Configuração

1. Clone o repositório:
    ```sh
    git clone <URL_DO_REPOSITORIO>
    cd parodify-robot
    ```

2. Instale as dependências:
    ```sh
    pip install robotframework
    pip install robotframework-browser
    ```

3. Certifique-se de que o arquivo `module.js` está no diretório `resources`.

## Estrutura dos Testes

### Arquivo `player.robot`

O arquivo `player.robot` contém os testes automatizados. Aqui está um exemplo de um caso de teste:

```robot
*** Settings ***
Library   Browser    jsextension=${EXECDIR}/resources/module.js

Test Setup       Start session
Test Teardown    Finish session

*** Test Cases ***
Deve tocar uma musica
    ${song_name}    Set Variable    Smells Like Test Script
    Mock My Song
    Go to       https://parodify.vercel.app
    Get Text    css=.logged-user    contains    Fernando Papito
    ${play}    Get play button    ${song_name}
    ${pause}   Get pause button   ${song_name}
    Click    ${play}
    Wait For Elements State    ${pause}    visible   2
    Wait For Elements State    ${play}    visible   7

*** Keywords ***
Start session
    New Browser    browser=chromium   headless=False
    New Page    about:blank

Finish session
    Take Screenshot

Get play button
    [Arguments]        ${song_name}
    ${play}   Set Variable    
```

## Executando os Testes

Para executar os testes, use o comando:

```sh
robot player.robot
```

Os resultados dos testes serão gerados no diretório `logs/` nos arquivos `log.html`, `output.xml` e `report.html`.

## Logs e Relatórios

- `log.html`: Contém o log detalhado da execução dos testes.
- `output.xml`: Contém o resultado da execução dos testes em formato XML.
- `report.html`: Contém um relatório resumido da execução dos testes.

## Capturas de Tela

As capturas de tela são salvas no diretório `logs/browser/screenshot/`.

## Contribuição

Sinta-se à vontade para contribuir com este projeto. Abra uma issue ou envie um pull request.
