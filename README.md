# NESCOW: Non-native English Speaker's Co-Writer

<p align="center">
  <img src="nescow.png" alt="NESCOW Logo" width="150">
</p>

NESCOW は、英語を母語としない研究者や執筆者が、ローカルLLM（Ollama）を利用して英語論文の原稿をその場で逐次組み立てていくためのシングルページWebアプリケーション（HTML/JavaScript）です。

LLMによる英訳・校正を援用した執筆作業をローカル・オフライン環境下で進めることができます。

## 主な特徴

- **ローカル完結型**: Ollama経由でローカルLLMを利用するため、オフラインでも作業可能。執筆中の文章が外部サーバーに送信されることもありません。
- **インライン・逐次編成**: 1つの画面内で連続的に「元の文章」又は「LLMにより英訳・校正された文章」を「執筆中の論文原稿」に反映させられます。キーボードショートカットも利用可能。
- **単一ファイル構成**: Ollamaを始動させた後は1個のHTMLファイルをブラウザで開くだけで動作します。

## 事前準備

NESCOWを使用するには、ローカル環境で **Ollama** が動作している必要があります。インストール方法については https://ollama.com/download をご覧ください。
ローカルLLMをインストールします。NESCOWのデフォルトのものは以下のコマンドでインストールできます。
```powershell or bash
ollama pull phi4-mini gemma4:e2b qwen2.5-coder:7b
```

外部のHTMLファイルからOllamaのAPIにアクセスできるよう、CORS設定（`OLLAMA_ORIGINS`）を許可して起動してください。

### 💻 バッチファイルによるOllamaとNESCOW連続起動（Windows）
Windows環境では、`start_nescow.bat` によりOllamaとNESCOWの双方を起動させることが可能です。そのバッチファイルを実行する前にOllamaが動作している場合には、それを終了させて置く必要があります。

### Ollama起動コマンド例
*Ollamaが動作している場合には、それをコマンド実行前に終了させておく必要があります

**Windows (PowerShell):**
```powershell
$env:OLLAMA_ORIGINS="*"
ollama serve
```

**macOS / Linux (Terminal):**
```bash
OLLAMA_ORIGINS="*" ollama serve
```

## 使い方

1(ロゴを表示させたい場合のみ). `nescow.html` とロゴ画像（`nescow.png`）を同じフォルダに配置します。
2. 上述の起動コマンドでOllamaを起動します。
3. `nescow.html` を任意のWebブラウザで開きます。 *2と3はWindowsなら上述のバッチファイル（`nescow.html`と同じフォルダに配置）で連続実行可
4. 使用するOllamaのモデルを選択し（初期値：`phi4-mini` など）、テキスト入力欄に推敲したい文章を入力します。
5. 以下のキーボードショートカットまたは画面内のボタンを用いて、右側のエディタに原稿を組み立てていきます。

### キーボードショートカット

| 操作 | ショートカットキー | 挙動 |
| :--- | :--- | :--- |
| **校正の実行** | `Ctrl + Enter` | 入力欄の文章を論文調の英語に変換します。 |
| **校正【前】の追加（スペース結合）** | `Ctrl + Shift + Space` | 元の入力文章を、半角スペースを挟んで原稿末尾に追加します。 |
| **校正【前】の追加（改行結合）** | `Ctrl + Shift + Enter` | 元の入力文章を、改行して原稿末尾に追加します。 |
| **校正【後】の追加（スペース結合）** | `Ctrl + Space` | LLMによる変換結果を、半角スペースを挟んで原稿末尾に追加します。 |
| **校正【後】の追加（改行結合）** | `Ctrl + ↓` | LLMによる変換結果を、改行して原稿末尾に追加します。 |

## システムプロンプトについて

本ツールは内部でLLMに対し、以下の役割（システムプロンプト）を与えて要求を行っています。

> "You are an elite academic co-writer. Transform the input sentences into sophisticated, publication-ready academic English. Maintain the original sentence-by-sentence structure and logical meaning. Output ONLY the polished English sentence(s). Never include introductions, explanations, or quotes."

必要に応じて、HTMLファイル内の `systemPrompt` 変数の文字列を直接書き換えることで、生成される英文のトーンやスタイルをカスタマイズできます。

## ライセンス

[MIT License](LICENSE)

NESCOW is a single-page web application (HTML/JavaScript) designed for non-native English-speaking researchers and writers to compose academic manuscripts inline and incrementally using a local LLM (Ollama).

Since all processing is handled locally, your draft data is never sent to external servers.

## Features

- **Completely Local**: Uses Ollama to run LLMs locally, even under an offline condition.
- **Inline & Incremental Composition**: Input, polished results, and the main manuscript editor are contained in a single split-view window. Keyboard shortcuts allow you to transfer sentences into your draft seamlessly.
- **Single-File Setup**: No complex installation or server configuration is required. Open the single HTML file in any web browser.

## Prerequisites
Ollama needs to be installed in advance. Please see https://ollama.com/download for installation.
NESCOW default LLMs can be installed as follows.
```powershell or bash
ollama pull phi4-mini gemma4:e2b qwen2.5-coder:7b
```
To use NESCOW, **Ollama** must be running on your local machine. You also need to enable CORS by setting the `OLLAMA_ORIGINS` environment variable so that the browser application can access the Ollama API.

### Launching Ollama and NESCOW using a single batch (.bat) file (Windows only)

On Windows, Ollama and NESCOW can be sequentially launched by `start_nescow.bat`. *Existing Ollama session should be ended before the batch file is executed

### Startup Command Examples
*Existing Ollama session should be ended before these commands are run

**Windows (PowerShell):**
```powershell
$env:OLLAMA_ORIGINS="*"
ollama serve
```
**macOS / Linux (Terminal):**
```bash
OLLAMA_ORIGINS="*" ollama serve
```

## How to Use

1(only when the logo should be displayed). Place `nescow.html` and the logo image (`nescow.png`) in the same directory.
2. Start Ollama using the above command.
3. Open `nescow.html` in your web browser. *Steps 2 and 3 can be done by the above single `start_nescow.bat` file (in the same directory as `nescow.html`) on Windows
4. Select your Ollama model (e.g., `phi4-mini`) and enter your text into the input field.
5. Use the following keyboard shortcuts or on-screen buttons to build your manuscript in the right panel.

### Keyboard Shortcuts

| Action | Shortcut | Description |
| :--- | :--- | :--- |
| **Run Polish** | `Ctrl + Enter` | Transforms the input text into academic English. |
| **Append [Before] (with Space)** | `Ctrl + Shift + Space` | Appends the original input text to the manuscript, separated by a space. |
| **Append [Before] (with Newline)** | `Ctrl + Shift + Enter` | Appends the original input text to the manuscript with a line break. |
| **Append [After] (with Space)** | `Ctrl + Space` | Appends the polished result to the manuscript, separated by a space. |
| **Append [After] (with Newline)** | `Ctrl + ↓` | Appends the polished result to the manuscript with a line break. |

## System Prompt

The application sends the following instructions to the local LLM to guide its output:

> "You are an elite academic co-writer. Transform the input sentences into sophisticated, publication-ready academic English. Maintain the original sentence-by-sentence structure and logical meaning. Output ONLY the polished English sentence(s). Never include introductions, explanations, or quotes."

The tone and style of the generated English can be customized by directly modifying the `systemPrompt` variable inside the HTML file.

## License

[MIT License](LICENSE)
