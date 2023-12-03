# ComfyUI Telegram Bot

## Telegram bot for integrating ComfyUI

Functionalities include text2image, image2image, and LoRA support. IPAdapter enables face replacement and stylization.

Test bot: @Cryanalisis_bot

## Installation and Setup

Requires a working installation of ComfyUI with additional modules:

- ComfyUI-Impact-Pack
- ComfyUI_UltimateSDUpscale

Also requires the installation of segmentation models: *face_yolov8m.pt*

Upscaler: *4xNMKDSuperscale_4xNMKDSuperscale.pt*

ControlNet model: *control_v11f1e_sd15_tile.pth*

Copy the file `default_lora.safetensors` from the assets directory to your LoRA directory. This is a workaround for workflows without LoRA.

Rename the `config.yaml.sample` file to `config.yaml` and configure it as follows:

(See the code snippet for the configuration)

## Work Description

Workflows are used for generation, and they are in the ComfyUI API format within the 'workflows' directories.

By default, receiving a clean prompt generates an image with dimensions DEFAULT_WIDTH x DEFAULT_HEIGHT. You can specify the size in the format WIDTHxHEIGHT.

The bot's response includes two messages: an image (with quality loss due to Telegram compression) and a PNG file with the original quality.

If an image is sent to the bot, it will be transformed according to the prompt, such as commands `/face`, `/upscale`. Note! ControlNet is used for img2img instead of classical denoise, providing results closer to the original.

To add your negative prompt instead of the built-in one, append it to the message using a separator `|`.

Example of a complete prompt (image2image) with sending a reference image:

(See the code snippet for the example)

(Images showing original and resulting transformations are described)

Images sent to the bot are saved in the 'upload' directory, and the generated results are in the 'generated' directory.

## Additional Commands

Commands include specifying the number of sampler steps `%50`, setting image2image ControlNet strength `$0.5`, listing models `/models`, and listing available LoRAs `/loras`.

## Access Limitation

Utilizes a whitelist. If the whitelist in `config.yaml` is empty, access is open to everyone. Add the Telegram UID of allowed users to the list.

(See the code snippet for the whitelist configuration)

## Using LoRA

Add your lines in the `loras` section in `config.yaml`. LoRA is connected by adding `#LoRA_name` to the prompt. For instance, `#vlozhkin`. You can specify strength like `#lora_name:0.5`.

LoRA line format: `bot's name` | `LoRA model file name` | `default strength` | `string added at the beginning of the prompt`

Example:

(See the code snippet for the LoRA configuration)

---
