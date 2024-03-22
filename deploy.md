gcloud artifacts repositories describe sample --project=flawless-window-258300 --location=asia-northeast1


gcloud artifacts repositories create sample --location asia-northeast1 --repository-format "docker" --description "sample"
gcloud auth configure-docker

gcloud builds submit --config ./build/cloudbuild.yaml ./docker/php　
gcloud run jobs deploy reacquisition-batch-job --region=asia-northeast1 --image=asia-northeast1-docker.pkg.dev/tcdp-dev/reacquisition-batch/reacquisition-batch:1.0 --task-timeout 3600 --cpu=1 --memory=512Mi --parallelism=1 --env-vars-file=./deploy/dev/dev_env.yaml --set-cloudsql-instances=tcdp-dev:asia-northeast1:tcdp-dev002 --service-account=tcdp-dev@appspot.gserviceaccount.com