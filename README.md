
-------

# My Own AI

*A simple LLM - to run on your own machines - for developers who want easy set up of their own AI for projects*

As a software developer and entrepreneur in the 20s,  
I want AI intergration into my various projects.  

I don't need a super intelligent model,  
but I want one that I can run myself.

I want to provide custom training, or at least context,   
and I want API access to it.   

This repo is my attempt at achieving this vision for myself.

I'll update the README with usage notes and details as we progress along.


-------

## Ollama LLM/AI Setup

1. Install Ollama : https://ollama.com/download


```
curl -fsSL https://ollama.com/install.sh | sh
```


2. Install your model. There are [many](https://ollama.com/library) to choose from, I started with : https://ollama.com/library/orca-mini

```
ollama run orca-mini
```

This is a command-line chat interface.   
Worth trying to ensure you are set up Ok to this point, but we are then going to use the API interface.

3. Test the API interface:

```
curl -X POST http://localhost:11434/api/generate \
  -H 'Content-Type: application/json' \
  -d '{
    "model": "orca-mini",
    "prompt": "Tell me a short story about a robot learning to paint.",
    "stream": false
  }'
```


-------

## Public API (with Auth and Key Manager)

I want to make the AI bots I create available to others,  
And I want to rate-limit what they can hit my APIs with,
So next I'm setting something up so that they can create API Keys,
 (and pay to get extra usage on them).

I'm investigating "Lago" : https://github.com/getlago/lago    

```
# Get the code
git clone https://github.com/getlago/lago.git

# Go to Lago folder
cd lago

# Set up environment configuration
echo "LAGO_RSA_PRIVATE_KEY=\"`openssl genrsa 2048 | base64`\"" >> .env
source .env

# Start the api
docker compose up -d api

# Create the database
docker compose exec api rails db:create
docker compose exec api rails db:migrate

# Start all other components
docker compose up
```


.... WIP ... 


