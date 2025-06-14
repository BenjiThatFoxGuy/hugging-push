# hugging-push

GitHub action that'll push files of the current github code repository to the hugging face space code repository.


## Usage

The first step is to add a Hugging Face token with write access to your repo as a GitHub Secret. Below, which is called HF_TOKEN. Then, you can use this action in your repo as shown below. 

```yaml
name: Deploy to huggingface

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: BenjiThatFoxGuy/hugging-push@v0.2.4
        with:
          # The Hugging Face repo id you want to sync to.
          # A repo with this name will be created if it doesn't exist. Required.
          # The github username is not included. ex: not like this 'username/reponame', but like this: 'reponame'
          # the key of huggingface_repo can be omitted. If the key is commented out, it defaults to the same name as the Github repository. 
          # huggingface_repo: 'ChatGPT'

          # Hugging Face token with write access. Required.
          # Here, we provide a token that we called `HF_TOKEN` when we added the secret to our GitHub repo.
          hf_token: ${{ secrets.HF_TOKEN }}

          # The type of repo you are syncing to: model, dataset, or space.
          # Defaults to space.
          repo_type: 'space'
  
          # If true and the Hugging Face repo doesn't already exist, it will be created
          # as a private repo.
          #
          # Note: this param has no effect if the repo already exists.
          private: false

          # If repo type is space, specify a space_sdk. One of: streamlit, gradio, or static
          #
          # This option is especially important if the repo has not been created yet.
          # It won't really be used if the repo already exists.
          space_sdk: 'gradio'
```

> `- uses: actions/checkout@v2` is not needed, because it's already included in this Action. BenjiThatFoxGuy/hugging-push