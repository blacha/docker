# Hugo + Go + GCloud SDK


Pipeline to deploy static sites made with hugo into Google cloud Storage.



```
branches:
    master:
      - step:
        script:
          - hugo
          # GCloud Auth
          - echo $GCLOUD_API_KEY | base64 --decode --ignore-garbage > ./gcloud-api-key.json
          - gcloud auth activate-service-account --key-file gcloud-api-key.json
          # Linking to the Google Cloud project
          - gcloud config set project $PROJECT_NAME
          # Deploy to dev
          - gsutil -m rsync -r public/ gs://$DEV_BUCKET_NAME/

```