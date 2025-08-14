# Newsroom archive assistant GPT tutorial

Tutorial on how to set up your newsroom's archive search assistant using OpenAI's custom GPT.

Basic setup:
-

- Go to "GPTs" --> "My GPT" --> hit "Create"
- Give your GPT a name (mine is "Article Search Bot")
- Give your GPT a description
<img width=600 height=auto alt="Screenshot 2025-08-13 at 3 37 11 PM" src="https://github.com/user-attachments/assets/f21455dd-c8d5-4551-8fb1-644874b377e8" />

  
Instructions: 
-

Copy and paste the prompt into the instruction box. **Alter the prompt** based on your newsroom/organization's needs. 

For the **categories_exclude** command, we are telling the chatbot to exclude all sponsored content on Sahan's website using the corresponding WordPress category ID. You can omit this part, or exclude other category ID based on your newsroom's API structure. Read more about WordPress API categories [here](https://developer.wordpress.org/rest-api/reference/categories/).
 
    You are a marketing associate at Sahan Journal, a nonprofit newsroom serving Minnesota's immigrants and communities of color. You are meeting with potential clients to have them advertise on Sahan Journal's platform. You are tasked to look at articles published in Sahan Journal and find relevant articles to the client's product/program/industry. 
    
    When the user asks you to find recent stories related to a topic, use the associated Action script to search for relevant stories via Sahan Journal's WordPress API. When you call the API, limit the _fields you request to "id,title,excerpt,date,slug,status,link" and add "categories_exclude": "2514"
    
    For each article, please provide:
    - Article title
    - A short summary of the article
    - Publish date
    - URL of the article 
    
    Give the users 3 articles by default. If the user asks for more than 3 articles, provide the number of articles as requested.
    Only provide information based on the API call. Do not fabricate or make up articles.

    

GPT Action Script (for WordPress sites)
-

Click on “Create new action,” and insert the action script (see [`newsroom-archive-setup.txt`](https://github.com/sahanjournal/newsroom-archive-gpt/blob/main/newsroom-archive-setup.txt)) into the schema in your GPT configuration.

<img width="600" height=auto alt="Screenshot 2025-08-13 at 3 06 56 PM" src="https://github.com/user-attachments/assets/3a93b724-a3ff-45d0-b30b-b1e69b5c86fd" />


🔴**Important**🔴: Make sure to **modify this part of the script** and insert your organization's **name and url**. 


    openapi: 3.1.0
    info:
      title: [Newsroom Name] Post API 
      description: API for retrieving [Newsroom Name] Posts via the REST API.
      version: 1.0.0
    servers:
      - url: [Newsroom site url]/wp-json/wp/v2 
        description: [Newsroom Name] REST API server

Once you've inserted the script, you should see the “Available actions” pop up below the script.

<img width="600" height=auto alt="Screenshot 2025-08-13 at 3 22 23 PM" src="https://github.com/user-attachments/assets/6f3d9f74-b979-4998-962b-bea20bfaad9f"  />




### 🥳Congrats! You just set up the archive bot!
This is what the output (usually) looks like:

<img width=700 height=auto alt="Screenshot 2025-08-13 at 3 17 32 PM" src="https://github.com/user-attachments/assets/111c8eb9-5168-4701-8cb2-c8c723c392e0" />


Important note:
-

Make sure to disable the Web Search function if you want to prevent the GPT from drawing sources from the internet.
