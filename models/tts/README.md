# Deploy a Text-to-Speech Service with Docker

This tutorial demonstrates how you can deploy a single-container Text-to-Speech (TTS) service on your local machine using Docker.

*Please Note: these images take a while to load. It can take upto 10 minutes on the first run to pull everything.*

## Prerequisites

- Ensure you have your [entitlement key](https://myibm.ibm.com/products-services/containerlibrary) to access the IBM Entitled Registry. [Get a Watson Text to Speech trial license](https://www.ibm.com/account/reg/us-en/subscribe?formid=urx-51758).
- [Docker](https://docs.docker.com/get-docker/) is installed.

**Tip**:

- [Podman](https://podman.io/getting-started/installation) provides a Docker-compatible command line front end. Unless otherwise noted, all the the Docker commands in this tutorial should work for Podman, if you simply alias the Docker CLI with `alias docker=podman` shell command.

## Steps

### Step 1: Login to the IBM Entitled Registry

IBM Entitled Registry contains various container images for Watson Speech. Once you've obtained the entitlement key from the [container software library](https://myibm.ibm.com/products-services/containerlibrary), you can login to the registry with the key, and pull the container images to your local machine.

```sh
echo $IBM_ENTITLEMENT_KEY | docker login -u cp --password-stdin cp.icr.io
```

### Step 2: Ensure you're in the correct directory

Make sure when building the STT model, you're terminal is correctly in the `stt` directory, so that you target the `Dockerfile` and context for the Dockerfile.

### Step 3. Build the container image

Build a container image with the provided `Dockerfile`. The containers serve multiple pretrained models. Additional models can be added to support other languages by updating the provided `Dockerfile`, as well as `env_config.json` and `sessionPools.yaml` in the `config` directory.

```sh
docker build . -t tts-standalone
```

### Step 4. Run the service

You can run the container on Docker as follows, using the container image created in the previous step.

```sh
docker run --rm -it --env ACCEPT_LICENSE=true --publish 1081:1080 tts-standalone
```

This runs the service in the foreground.

### Step 5. Test the service

Open up another terminal. First, query the models that are available from the service.

```sh
curl "http://localhost:1081/text-to-speech/api/v1/voices"
```

You will see output similar to the following.

```json
{
    "voices": [
        {
            "name": "en-US_MichaelV3Voice",
            "language": "en-US",
            "gender": "male",
            "description": "Michael: American English male voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_MichaelV3Voice"
        },
        {
            "name": "en-US_EmilyV3Voice",
            "language": "en-US",
            "gender": "female",
            "description": "Emily: American English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_EmilyV3Voice"
        },
        {
            "name": "fr-CA_LouiseV3Voice",
            "language": "fr-CA",
            "gender": "female",
            "description": "Louise: French Canadian female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/fr-CA_LouiseV3Voice"
        },
        {
            "name": "en-US_OliviaV3Voice",
            "language": "en-US",
            "gender": "female",
            "description": "Olivia: American English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_OliviaV3Voice"
        },
        {
            "name": "it-IT_FrancescaV3Voice",
            "language": "it-IT",
            "gender": "female",
            "description": "Francesca: Italian (italiano) female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/it-IT_FrancescaV3Voice"
        },
        {
            "name": "en-US_AllisonV3Voice",
            "language": "en-US",
            "gender": "female",
            "description": "Allison: American English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_AllisonV3Voice"
        },
        {
            "name": "fr-FR_ReneeV3Voice",
            "language": "fr-FR",
            "gender": "female",
            "description": "Renee: French (français) female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/fr-FR_ReneeV3Voice"
        },
        {
            "name": "en-GB_JamesV3Voice",
            "language": "en-GB",
            "gender": "male",
            "description": "James: British English male voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-GB_JamesV3Voice"
        },
        {
            "name": "en-US_LisaV3Voice",
            "language": "en-US",
            "gender": "female",
            "description": "Lisa: American English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_LisaV3Voice"
        },
        {
            "name": "en-US_KevinV3Voice",
            "language": "en-US",
            "gender": "male",
            "description": "Kevin: American English male voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_KevinV3Voice"
        },
        {
            "name": "en-US_HenryV3Voice",
            "language": "en-US",
            "gender": "male",
            "description": "Henry: American English male voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-US_HenryV3Voice"
        },
        {
            "name": "en-GB_CharlotteV3Voice",
            "language": "en-GB",
            "gender": "female",
            "description": "Charlotte: British English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-GB_CharlotteV3Voice"
        },
        {
            "name": "fr-FR_NicolasV3Voice",
            "language": "fr-FR",
            "gender": "male",
            "description": "Nicolas: French (français) male voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/fr-FR_NicolasV3Voice"
        },
        {
            "name": "en-GB_KateV3Voice",
            "language": "en-GB",
            "gender": "female",
            "description": "Kate: British English female voice. Dnn technology.",
            "customizable": true,
            "supported_features": {
                "custom_pronunciation": true,
                "voice_transformation": false
            },
            "url": "http://localhost:1081/text-to-speech/api/v1/voices/en-GB_KateV3Voice"
        }
    ]
}
```

Generate an audio file in English.

```sh
curl "http://localhost:1081/text-to-speech/api/v1/synthesize" \
  --header "Content-Type: application/json" \
  --data '{"text":"Hello world"}' \
  --header "Accept: audio/wav" \
  --output output.wav
```

Then output will be in `output.wav`.

Next, try the French model.

```sh
curl "http://localhost:1081/text-to-speech/api/v1/synthesize?voice=fr-CA_LouiseV3Voice" \
  --header "Content-Type: application/json" \
  --data '{"text":"Bonjour le monde."}' \
  --header "Accept: audio/wav" \
  --output french-test.wav
```

The output will be in `french-test.wav`.

## Acknowledgements

This repository was created based off the [IBM Build Lab Watson Speech repository](https://github.com/ibm-build-lab/Watson-Speech). Specifically, their `single-container-tts` directory.