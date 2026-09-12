# ComfyUI LLM Text Processor (fork)

更新日: 2026-09-12

## 概要

ローカル GGUF LLM でプロンプト作成・書き換え・翻訳・キャプション・抽出などのテキスト処理を行うノードです。ComfyUI-LLM-text-processorのfork版です。マルチモーダルモデルでは画像（または画像バッチ）と `mmproj` も渡せます。応答と推論過程は別出力です。ノードの基本動作は上流 [ComfyUI-LLM-text-processor](https://github.com/KingManiya/ComfyUI-LLM-text-processor) と同じです。使い方は上流 README を参照してください。

推論は `llama-cli` で行い、バイナリ取得は [ComfyUI-llama-cli](../ComfyUI-llama-cli) に任せます。未導入なら `Install custom_nodes/ComfyUI-llama-cli and restart ComfyUI.` で止まります。

## 差分

- **llama-cli**: このフォークは推論だけ行う。取得ロジックは持たない。
- **`keep_in_ram`**: 生成後も GGUF（と選択中の mmproj）を DRAM に残し、次回の GPU ロードを速くする。既定は OFF。VRAM は毎回空く。KV キャッシュは残さない。ロック（`VirtualLock` / `mlock`）に失敗しても実行は止めない。
- 実行時は共有ライブラリ用に `LD_LIBRARY_PATH` を付与する。

ComfyUI Manager の `LLM Text Processor`（pack `comfyui-llm-text-processor`、クラス `LLMTextProcessor`）は上流本体です。このフォークは別 pack（`comfyui-llm-text-processor-fork`）・別ノード（`LLM Text Processor (fork)` / `LLMTextProcessorFork`）です。使う場合はこのリポジトリと `ComfyUI-llama-cli` を `custom_nodes` に置いてください。既存ワークフローの上流ノードは差し替えが必要です。
