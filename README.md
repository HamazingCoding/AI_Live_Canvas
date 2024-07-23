# AI Canvas Generation

AI Canvas Generation is a Unity Application that utilizes advanced machine learning techniques to create and manipulate images. The project leverages models like Stable Diffusion, CLIP, VAE, and ControlNet to provide an interactive and versatile canvas for image generation and transformation.

## Features

- **Load Checkpoints**: Load various models including Stable Diffusion and custom checkpoints.
- **Text Encoding**: Use CLIP to encode text prompts for image generation.
- **Noise Addition**: Add noise to images for enhanced creativity and experimentation.
- **VAE Encoding/Decoding**: Encode and decode images using VAE for latent space manipulation.
- **Sampler Customization**: Utilize custom samplers for fine-tuned image generation.
- **ControlNet Application**: Apply ControlNet models for advanced image control and manipulation.
- **Image Scaling and Saving**: Upscale and save generated images for further use.

## Installation

To run this project, you need to have Python installed on your system. Follow the steps below to set up the project:

1. **Clone the Repository**

    ```sh
    git clone https://github.com/yourusername/ai-canvas-generation.git
    cd ai-canvas-generation
    ```

2. **Install Dependencies**

    Create a virtual environment (optional but recommended):

    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

    Install the required packages:

    ```sh
    pip install -r requirements.txt
    ```

3. **Download Models**

    Make sure to download the required models and place them in the appropriate directories as specified in the configuration files or scripts. Some of the models you may need include:

    - Stable Diffusion checkpoint (`toonAme_version20.safetensors`)
    - LoRA weights (`LCM_LoRA_Weights_SDXL.safetensors`)
    - VAE models (`vaeFtMse840000EmaPruned_vae.safetensors`)

    Refer to the scripts for the exact model names and locations.

## Usage

1. **Run the Application**

    ```sh
    python main.py
    ```

2. **Generate Images**

    Follow the prompts in the application or modify the scripts to input your own text prompts and parameters for image generation. Here is an example of a JSON configuration that you can use:

    ```json
    {
      "4": {
        "inputs": {
          "ckpt_name": "toonAme_version20.safetensors"
        },
        "class_type": "CheckpointLoaderSimple",
        "_meta": {
          "title": "Load Checkpoint"
        }
      },
      "6": {
        "inputs": {
          "text": "Pprompt",
          "clip": [
            "10",
            0
          ]
        },
        "class_type": "CLIPTextEncode",
        "_meta": {
          "title": "CLIP Text Encode (Prompt)"
        }
      },
      "7": {
        "inputs": {
          "text": "Nprompt",
          "clip": [
            "10",
            0
          ]
        },
        "class_type": "CLIPTextEncode",
        "_meta": {
          "title": "CLIP Text Encode (Prompt)"
        }
      },
      "8": {
        "inputs": {
          "samples": [
            "49",
            0
          ],
          "vae": [
            "92",
            0
          ]
        },
        "class_type": "VAEDecode",
        "_meta": {
          "title": "VAE Decode"
        }
      },
      "10": {
        "inputs": {
          "stop_at_clip_layer": -1,
          "clip": [
            "4",
            1
          ]
        },
        "class_type": "CLIPSetLastLayer",
        "_meta": {
          "title": "CLIP Set Last Layer"
        }
      },
      "49": {
        "inputs": {
          "seed": 632193426615121,
          "steps": 10,
          "cfg": 1.6,
          "sampler_name": "euler_ancestral",
          "scheduler": "normal",
          "denoise": 0.78,
          "model": [
            "56",
            0
          ],
          "positive": [
            "6",
            0
          ],
          "negative": [
            "7",
            0
          ],
          "latent_image": [
            "54",
            0
          ]
        },
        "class_type": "KSampler",
        "_meta": {
          "title": "KSampler"
        }
      },
      "54": {
        "inputs": {
          "pixels": [
            "59",
            0
          ],
          "vae": [
            "92",
            0
          ]
        },
        "class_type": "VAEEncode",
        "_meta": {
          "title": "VAE Encode"
        }
      },
      "55": {
        "inputs": {
          "lora_name": "LCM_LoRA_Weights_SDXL.safetensors",
          "strength_model": 1,
          "strength_clip": 1,
          "model": [
            "4",
            0
          ],
          "clip": [
            "4",
            1
          ]
        },
        "class_type": "LoraLoader",
        "_meta": {
          "title": "Load LoRA"
        }
      },
      "56": {
        "inputs": {
          "sampling": "lcm",
          "zsnr": false,
          "model": [
            "55",
            0
          ]
        },
        "class_type": "ModelSamplingDiscrete",
        "_meta": {
          "title": "ModelSamplingDiscrete"
        }
      },
      "59": {
        "inputs": {
          "image_path": "C:\\Users\\Sparkslab-Laptop\\Desktop\\Repos\\ComfyUI\\custom_nodes\\ComfyUI_toyxyz_test_nodes\\CaptureCam\\captured_frames\\capture.jpg"
        },
        "class_type": "LoadWebcamImage",
        "_meta": {
          "title": "Load Webcam Image"
        }
      },
      "60": {
        "inputs": {
          "upscale_method": "nearest-exact",
          "width": 1024,
          "height": 1024,
          "crop": "disabled",
          "image": [
            "8",
            0
          ]
        },
        "class_type": "ImageScale",
        "_meta": {
          "title": "Upscale Image"
        }
      },
      "91": {
        "inputs": {
          "filename_prefix": "ComfyUI",
          "images": [
            "60",
            0
          ]
        },
        "class_type": "SaveImage",
        "_meta": {
          "title": "Save Image"
        }
      },
      "92": {
        "inputs": {
          "vae_name": "vaeFtMse840000EmaPruned_vae.safetensors"
        },
        "class_type": "VAELoader",
        "_meta": {
          "title": "Load VAE"
        }
      }
    }
    ```

3. **Save and Preview Images**

    The generated images will be saved in the specified directory, and you can preview them using the provided scripts or your preferred image viewer.

## Contributing

Contributions are welcome! If you have any suggestions, bug reports, or feature requests, feel free to open an issue or submit a pull request.

## Acknowledgements

- [Stable Diffusion](https://github.com/CompVis/stable-diffusion)
- [CLIP](https://github.com/openai/CLIP)
- [ControlNet](https://github.com/lllyasviel/ControlNet)

## Contact

If you have any questions or need further assistance, please contact me at [hamazing174@gmail.com].
