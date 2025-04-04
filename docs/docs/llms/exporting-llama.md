---
title: Exporting Llama
sidebar_position: 2
---

In order to make the process of export as simple as possible for you, we created a script that runs a Docker container and exports the model.

## Steps to export Llama

### 1. Create an account

Get a [HuggingFace](https://huggingface.co/) account. This will allow you to download needed files. You can also use the [official Llama website](https://www.llama.com/llama-downloads/).

### 2. Select a model

Pick the model that suits your needs. Before you download it, you'll need to accept a license. For best performance, we recommend using Spin-Quant or QLoRA versions of the model:

- [Llama 3.2 3B](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct/tree/main/original)
- [Llama 3.2 1B](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct/tree/main/original)
- [Llama 3.2 3B Spin-Quant](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct-SpinQuant_INT4_EO8/tree/main)
- [Llama 3.2 1B Spin-Quant](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct-SpinQuant_INT4_EO8/tree/main)
- [Llama 3.2 3B QLoRA](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct-QLORA_INT4_EO8/tree/main)
- [Llama 3.2 1B QLoRA](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct-QLORA_INT4_EO8/tree/main)

### 3. Download files

Download the `consolidated.00.pth`, `params.json` and `tokenizer.model` files. If you can't see them, make sure to check the `original` directory.

### 4. Rename the tokenizer file

Rename the `tokenizer.model` file to `tokenizer.bin` as required by the library:

```bash
mv tokenizer.model tokenizer.bin
```

### 5. Run the export script

Navigate to the `llama_export` directory and run the following command:

```bash
./build_llama_binary.sh --model-path /path/to/consolidated.00.pth --params-path /path/to/params.json
```

The script will pull a Docker image from Docker Hub, and then run it to export the model. By default the output (llama3_2.pte file) will be saved in the `llama-export/outputs` directory. However, you can override that behavior with the `--output-path [path]` flag.

:::note
This Docker image was tested on MacOS with ARM chip. This might not work in other environments.
:::
