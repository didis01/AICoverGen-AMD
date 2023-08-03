# AICoverGen
An autonomous pipeline to create covers with any RVC v2 trained AI voice from YouTube videos. For developers who may want to add a singing functionality into their AI assistant/chatbot/vtuber, or for people who want to hear their favourite characters sing their favourite song. (ONLY AMD and LINUX)

![](images/webui_generate.png?raw=true)

This setup guide is tested for Linux Mint 21.1

## Setup

### Install Python

Python **VERSION 3.10** if you haven't already. Using other versions of Python may result in dependency conflicts.

### Install ffmpeg

Follow the instructions [here](https://www.hostinger.com/tutorials/how-to-install-ffmpeg) to install ffmpeg on your computer.

### Install ROCm

Open the file ROCm_Setup and follow the instructions.

### Download this repository

Open a command line window and run these commands to clone this entire repository and install the additional dependencies required.

```
cd AICoverGen
pip install -r requirements.txt
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm5.4.2
```

### Download required models

Run the following command to download the required MDXNET vocal separation models and hubert base model.

```
python src/download_models.py
```


## Usage with WebUI

To run the AICoverGen WebUI, run the following command.

```
python src/webui.py
```

Once the following output message `Running on local URL:  http://127.0.0.1:7860` appears, you can click on the link to open a tab with the WebUI.

### Download RVC models via WebUI

![](images/webui_dl_model.png?raw=true)

Navigate to the `Download model` tab, and paste the download link to the RVC model and give it a unique name.
You may search the [AI Hub Discord](https://discord.gg/aihub) where already trained voice models are available for download. You may refer to the examples for how the download link should look like.
The downloaded zip file should contain the .pth model file and an optional .index file.

Once the 2 input fields are filled in, simply click `Download`! Once the output message says `[NAME] Model successfully downloaded!`, you should be able to use it in the `Generate` tab!


### Running the pipeline via WebUI

![](images/webui_generate.png?raw=true)

- From the Voice Models dropdown menu, select the voice model to use. Click `Update` if you added the files manually to the [rvc_models](rvc_models) directory to refresh the list.
- In the YouTube link field, copy and paste the link to any song on YouTube.
- Pitch should be set to either -12, 0, or 12 depending on the original vocals and the RVC AI modal. This ensures the voice is not *out of tune*.

Once all fields are filled in, click `Generate` and the AI generated cover should appear in a less than a few minutes depending on your GPU.

## Usage with CLI

### Manual Download of RVC models

Unzip (if needed) and transfer the `.pth` and `.index` files to a new folder in the [rvc_models](rvc_models) directory. Each folder should only contain one `.pth` and one `.index` file.

The directory structure should look something like this:
```
├── rvc_models
│   ├── John
│   │   ├── JohnV2.pth
│   │   └── added_IVF2237_Flat_nprobe_1_v2.index
│   ├── May
│   │   ├── May.pth
│   │   └── added_IVF2237_Flat_nprobe_1_v2.index
│   ├── MODELS.txt
│   └── hubert_base.pt
├── mdxnet_models
├── song_output
└── src
 ```

### Running the pipeline

To run the AI cover generation pipeline using the command line, run the following command.

```
python src/main.py -yt YOUTUBE_LINK -dir MODEL_DIR_NAME -p PITCH_CHANGE
```

- Replace YOUTUBE_LINK with any link to a song on YouTube. Link should be enclosed in double quotes for Windows and single quotes for Unix-like systems
- Replace MODEL_DIR_NAME with the name of the folder in the [rvc_models](rvc_models) directory containing your `.pth` and `.index` files.
- Replace PITCH_CHANGE with 0 for no change in pitch to the AI vocals. Generally use 12 for male to female conversions or -12 for vice-versa.


## Terms of Use

The use of the converted voice for the following purposes is prohibited.

* Criticizing or attacking individuals.

* Advocating for or opposing specific political positions, religions, or ideologies.

* Publicly displaying strongly stimulating expressions without proper zoning.

* Selling of voice models and generated voice clips.

* Impersonation of the original owner of the voice with malicious intentions to harm/hurt others.

* Fraudulent purposes that lead to identity theft or fraudulent phone calls.

## Disclaimer

I am not liable for any direct, indirect, consequential, incidental, or special damages arising out of or in any way connected with the use/misuse or inability to use this software.
