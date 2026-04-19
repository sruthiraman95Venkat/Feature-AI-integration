AI powered Identity provisioning Teams Bot
## Overview
AI agent that accepts natural language from employees via teams and uses Open AI to understand the request and gets the manager approval and automatically provisions access across cloud and on-premise environments

Azure Resources: 
Resource Group: rg-ai-provisioning
Azure Open AI: oai-ai-provisioning
Model: GPT 4.1 mini 
Day 1: Azure Open AI resource created
GPT 4.1 mini model deployed (Since it does not involve complex reasoning and considering the cost here we are going with mini model, also they tend to respond faster)
<img width="1058" height="867" alt="image" src="https://github.com/user-attachments/assets/fcd0e151-d7b2-4b5e-97f4-09338d4e7d1c" />
<img width="635" height="610" alt="image" src="https://github.com/user-attachments/assets/b6c86f61-cf98-474c-851b-80f612994330" />
Encountered the error
<img width="659" height="892" alt="image" src="https://github.com/user-attachments/assets/c4a4c333-061b-41c3-b429-16263eb6c2a9" />
So changed the deployment type from Global Standard to Standard and changed the Tokens per minute limit to 10K 
Testing the model, can confirm that its working for Finance, IT and sales 
Model tested - department extraction working for Finance, HR, IT, Sales
<img width="1364" height="872" alt="image" src="https://github.com/user-attachments/assets/38a1fc3f-799f-4920-bf30-567a8b980a0b" />
Day 2: Copied the Open AI Endpoint URL and the key 
Created the Azure Bot, 
<img width="821" height="757" alt="image" src="https://github.com/user-attachments/assets/c9716b8b-43e8-44fb-a6b6-9b2ad2397ca7" />
<img width="874" height="480" alt="image" src="https://github.com/user-attachments/assets/7b2ef64f-93be-40e1-b0e5-ffe51a697aad" />
Enabling the Teams channel on Bot:
<img width="900" height="898" alt="image" src="https://github.com/user-attachments/assets/16f52a95-b7fd-46ff-8619-9a36c2f9fa45" />
Installing Azure core functions on the laptop 
npm install -g azure-functions-core-tools@4 --unsafe-perm true
Day 3: Initiating Azure Functions within python:
mkdir bot-ai-provisioning
cd bot-ai-provisioning
func init --python
Noticed that the below files were created
Writing requirements.txt
Writing function_app.py
Writing .gitignore
Writing host.json
Writing local.settings.json
Writing C:\Users\Sruthi\OneDrive\botAIProvisioning\bot-ai-provisioning\.vscode\extensions.json
Creating the actual function inside Python:
func new --name HttpTrigger --template "HTTP trigger" --authlevel anonymous
This command creates a new function within Python by the name "HttpTrigger" which uses the existing template "HTTP Tigger"
--authlevel anonymous - meaning anyone can call this function without a key, In Prod we would set it as function or admin so only specific users can trigger the function
Opened the project in VSCode and under function_app.py will be the default template code that Azure creates. 
Installed the required Python libraries
pip install azure-functions openai requests
Run the script and understood what it does
## Azure Function (bot-ai-provisioning)

### What it does:
Receives a message from the Teams bot, sends it to Azure OpenAI 
to extract the department, then triggers the Logic App webhook 
to provision the user.

### Flow:
1. Receives message + username from Teams bot
2. Sends message to GPT-4.1-mini to extract department
3. Calls Logic App webhook with username + department
4. Returns confirmation message

### Files:
- `function_app.py` — main function code
- `local.settings.json` — local config (not pushed to Git)
- `requirements.txt` — Python dependencies
- `host.json` — Azure Function settings

### Status:
- [x] Azure Function created
- [x] OpenAI integration coded
- [x] Logic App webhook connected
- [ ] Tested locally
- [ ] Deployed to Azure
- [ ] Connected to Teams bot







