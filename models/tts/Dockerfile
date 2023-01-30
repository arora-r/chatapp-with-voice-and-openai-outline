# Model images
FROM cp.icr.io/cp/ai/watson-tts-generic-models:1.1.0 AS catalog
# Add additional models here
FROM cp.icr.io/cp/ai/watson-tts-en-us-michaelv3voice:1.1.0 AS michaelv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-henryv3voice:1.1.0 AS henryv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-gb-katev3voice:1.1.0 AS katev3voice
FROM cp.icr.io/cp/ai/watson-tts-en-gb-jamesv3voice:1.1.0 AS jamesv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-gb-charlottev3voice:1.1.0 AS charlottev3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-lisav3voice:1.1.0 AS lisav3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-kevinv3voice:1.1.0 AS kevinv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-emilyv3voice:1.1.0 AS emilyv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-allisonv3voice:1.1.0 AS allisonv3voice
FROM cp.icr.io/cp/ai/watson-tts-en-us-oliviav3voice:1.1.0 AS oliviav3voice
FROM cp.icr.io/cp/ai/watson-tts-fr-ca-louisev3voice:1.1.0 AS louisev3voice
FROM cp.icr.io/cp/ai/watson-tts-fr-fr-reneev3voice:1.1.0 AS reneev3voice
FROM cp.icr.io/cp/ai/watson-tts-fr-fr-nicolasv3voice:1.1.0 AS nicolasv3voice
FROM cp.icr.io/cp/ai/watson-tts-it-it-francescav3voice:1.1.0 AS francescav3voice

# Base image for the runtime
FROM cp.icr.io/cp/ai/watson-tts-runtime:1.1.0 AS runtime

# Environment variable used for directory where configurations are mounted
ENV CONFIG_DIR=/opt/ibm/chuck.x86_64/var

# Copy in the catalog and runtime configurations
COPY --chown=watson:0 --from=catalog catalog.json ${CONFIG_DIR}/catalog.json
COPY --chown=watson:0 ./config/* ${CONFIG_DIR}/

# Intermediate image to populate the model cache
FROM runtime as model_cache

# Copy model archives from model images
RUN sudo mkdir -p /models/pool2

# For each additional models, copy the line below with the model image
COPY --chown=watson:0 --from=michaelv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=henryv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=katev3voice model/* /models/pool2/
COPY --chown=watson:0 --from=jamesv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=charlottev3voice model/* /models/pool2/
COPY --chown=watson:0 --from=lisav3voice model/* /models/pool2/
COPY --chown=watson:0 --from=kevinv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=emilyv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=allisonv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=oliviav3voice model/* /models/pool2/
COPY --chown=watson:0 --from=louisev3voice model/* /models/pool2/
COPY --chown=watson:0 --from=reneev3voice model/* /models/pool2/
COPY --chown=watson:0 --from=nicolasv3voice model/* /models/pool2/
COPY --chown=watson:0 --from=francescav3voice model/* /models/pool2/

# Run script to initialize the model cache from the model archives
COPY ./prepareModels.sh .

RUN ./prepareModels.sh

# Final runtime image with models baked in
FROM runtime as release

COPY --from=model_cache ${CONFIG_DIR}/cache/ ${CONFIG_DIR}/cache/