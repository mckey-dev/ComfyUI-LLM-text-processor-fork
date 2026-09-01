# ComfyUI LLM Text Processor (fork)

[KingManiya/ComfyUI-LLM-text-processor](https://github.com/KingManiya/ComfyUI-LLM-text-processor) のフォークです。ノードの基本動作は上流と同じです。使い方は上流 README を参照してください。

## 差分

- **Linux x64 CUDA**: 公式 CUDA バイナリが無いため、同じリリースタグのソースから `llama-cli` をビルドする。初回は `cmake` と `nvcc` が必要。以降は `vendor/llama.cpp/<tag>/linux-x64-cuda/` を再利用する。実行時は共有ライブラリ用に `LD_LIBRARY_PATH` を付与する。
- **Windows x64 CUDA 13**: 上流と同じ。公式リリース zip をダウンロードする。
- **`keep_in_ram`**: 生成後も GGUF（と選択中の mmproj）を DRAM に残し、次回の GPU ロードを速くする。既定は OFF。VRAM は毎回空く。KV キャッシュは残さない。ロック（`VirtualLock` / `mlock`）に失敗しても実行は止めない。

ComfyUI Manager の `LLM Text Processor` は上流本体です。本フォークを使う場合はこのリポジトリを `ComfyUI/custom_nodes` に置いてください。
