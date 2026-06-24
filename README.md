# Identificação de Metástase com CNN (ResNet18) — Grupo 7

Detecção de tecido **metastático** em imagens de histopatologia de linfonodos
(dataset **PatchCamelyon / PCam**), usando **transfer learning** com **ResNet18**.

> **Restrição do projeto:** roda **sem GPU** (apenas CPU). A ResNet18 pré-treinada é
> usada como **extrator de características congelado**; treinamos apenas uma pequena
> **cabeça classificadora**. Veja `COMO_FUNCIONA.md` para a explicação completa.

Todo o pipeline está em um único notebook: **`metastase_resnet18.ipynb`**.

---

## 1. Pré-requisitos

- **Python 3.10+** (testado no 3.12)
- ~2 GB livres em disco (ResNet18 pré-treinada + bibliotecas)
- O **dataset PCam** baixado (veja o passo 3)

---

## 2. Instalação

### Passo 2.1 — Abra um terminal na pasta do projeto
```bash
cd "~/Área de trabalho/PROJETO-FINAL-SISTEMAS_COMPUTACIONAIS"
```

### Passo 2.2 — Crie e ative um ambiente virtual
```bash
python3 -m venv venv
source venv/bin/activate
```
> No Windows seria `venv\Scripts\activate`. Aqui (Linux/Zorin) use o comando acima.

### Passo 2.3 — Instale as dependências
```bash
pip install --upgrade pip
pip install -r requirements.txt
```
> O `torch`/`torchvision` baixados são a versão **CPU** (não precisa de GPU).
> O download pode levar alguns minutos na primeira vez.

---

## 3. Onde colocar o dataset

O código detecta **automaticamente** um destes dois formatos. Ajuste o caminho na
**primeira célula** do notebook, na variável `DIR_DADOS`.

### Opção A — PCam oficial (.h5)  *(é o formato que usamos)*
Arquivos `camelyonpatch_level_2_split_*_x.h5` e `*_y.h5`.
No nosso caso estão em: `/home/andrey/Downloads/archive`.

### Opção B — Kaggle "Histopathologic Cancer Detection"
Pasta com `train_labels.csv` e `train/<id>.tif`.
Link: https://www.kaggle.com/competitions/histopathologic-cancer-detection/data

> Não precisa baixar tudo: o notebook sorteia um **subconjunto balanceado**
> (12.000 treino / 3.000 val / 3.000 teste). Ajuste em `N_TREINO`, `N_VAL`, `N_TESTE`.

---

## 4. Como executar

### Passo 4.1 — Abra o Jupyter
```bash
jupyter notebook metastase_resnet18.ipynb
```
> Vai abrir no navegador. (Também funciona pela extensão Jupyter do VS Code.)

### Passo 4.2 — Confira a 1ª célula
Verifique se `DIR_DADOS` aponta para a pasta do seu dataset.

### Passo 4.3 — Rode tudo
Menu **Run → Run All Cells** (ou rode célula por célula com `Shift+Enter`).

O notebook executa, na ordem:
1. **Configuração**
2. **Preparar** subconjunto balanceado do PCam
3. **Extrair features** com a ResNet18 congelada
4. **Treinar** a cabeça classificadora (com early stopping)
5. **Avaliar** no teste — imprime acurácia, AUC, precisão, recall, F1
6. **Gráficos** (inline): curvas de treino, matriz de confusão, curva ROC,
   histograma de separação e exemplos de previsões

> Todos os resultados aparecem **dentro do próprio notebook** — não é criada nenhuma
> pasta de saída. (A última célula, opcional, salva os pesos em `cabeca_treinada.pt`.)

##  Equipe
<table align="center">
  <tr>
    <td>
      <a href="https://github.com/andreysabino">
        <img src="https://avatars.githubusercontent.com/u/100762620?v=4" width="100px;" alt="Foto de Andrey Sabino no GitHub"/><br>
        <sub>
          <b>Andrey</b>
        </sub>
      </a>
    </td>
    <td>
      <a href="https://github.com/Joaofelype23">
        <img src="https://avatars.githubusercontent.com/u/110605331?v=4" width="100px;" alt="Foto de João Felype no GitHub"/><br>
        <sub>
          <b>João Felype</b>
        </sub>
      </a>
    </td>
    <td>
      <a href="https://github.com/Nathan-cardoso">
        <img src="https://avatars.githubusercontent.com/u/100364030?v=4" width="100px;" alt="Foto de Nathan Cardoso no GitHub"/><br>
        <sub>
          <b>Nathan Cardoso</b>
        </sub>
      </a>
    </td>
    <td>
      <a href="https://github.com/CaraChaato">
        <img src="https://avatars.githubusercontent.com/u/110605121?v=4" width="100px;" alt="Foto de Pedro Vinícius no GitHub"/><br>
        <sub>
          <b>Pedro Vinícius</b>
        </sub>
      </a>
    </td>
        </sub>
